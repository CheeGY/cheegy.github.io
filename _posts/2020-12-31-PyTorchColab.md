---
layout: post
title: "Recognizing Handwritten Digits with Machine Learning"
author: "Kong Yao"
categories: journal
tags: [machine learning]
image: post4.jpg
---
This post elaborates on a basic application of machine learning (ML) using PyTorch and Google Colab. 

---

## What is PyTorch?

PyTorch is a machine learning/deep learning open source library, based on the programming language, Python. It provides two main features; tensor computing through GPUs, as well as neural networks based on an automatic differentiation system.

## What is Google Colab?

[Google Colab] (https://colab.research.google.com/) is an web-based application that allows you to write and execute Python, right from your browser. Colab has several libraries pre-installed, including PyTorch. This allows users to use PyTorch in Colab, without any further installation.

---

## Example application - Handwritten Digits Recognition

One of the most explored applications in ML is the ability to recognize handwritten digits from images. For this example, we use the MNIST database, which contains images of handwritten digits (0 to 9). Here are some samples of these images,

![alt text](/assets/img/sample_mnist.PNG "MNIST samples")

As observed, some of these handwritten digits are more difficult to recognize than others. The objective of a ML model is to recognize these digits automatically, with high accuracy and without human supervision. Concretely, we first use part of the dataset to $\textbf{train}$ the ML model and allow it to learn the patterns/features of the images. Next, using what it has learnt, the model tries to predict the digits in the remaining images of the dataset. The first part of the dataset is often called the training dataset, while the second part of the dataset is called the validation dataset.

Before training the ML model, pre-processing is required to extract and partition the training and validation datasets and to normalize the database. The following code snippet performs this pre-processing, after importing the relevant libraries. 

```Python3
# Import PyTorch libraries
import torch
import torch.nn as nn
import torch.optim as optim
import torchvision as thv
from torch.utils.data import DataLoader, TensorDataset

device      = torch.device("cuda:0" if torch.cuda.is_available() else "cpu")

# Load the MNIST dataset from torchvision
train       = thv.datasets.MNIST('./', download=True, train=True)
val         = thv.datasets.MNIST('./', download=True, train=False)

# Reshape training and validation features from (batch_size,28,28) to (batch_size,28*28) and attach to GPU
xtrain      = train.data.view(-1, 28*28).to(device)
xval        = val.data.view(-1, 28*28).to(device)

# Normalize training and validation features from [0,255] to [0,1] 
xtrain      = xtrain/255.0
xval        = xval/255.0

# Attach training and validation labels to GPU
ytrain      = train.targets.to(device)
yval        = val.targets.to(device)

# Set training and validation dataloaders 
train_dataset     = TensorDataset(xtrain, ytrain)
train_dataloader  = DataLoader(train_dataset, batch_size=32, shuffle=True)

val_dataset       = TensorDataset(xval, yval)
val_dataloader    = DataLoader(val_dataset, batch_size=32,shuffle=False)
```

Another convenient thing about Colab and PyTorch is that this snippet above can be extracted directly into Colab and can be executed immediately.

----

Next, we construct a 1-layer linear neural network as our model.

```Python3
D_in, D_out   = 784, 10
model = torch.nn.Sequential(
    torch.nn.Linear(D_in, D_out),
    torch.nn.ReLU(),
).to(device)
```

---

Next, we implement the following training module, where the model is being trained. The cross entropy loss is used as the objective function and stochastic gradient descent (SGD) is used as the optimizer. 

```Python3
num_epochs    = 15
learning_rate = 0.08
criterion     = nn.CrossEntropyLoss()
optimizer     = torch.optim.SGD(model.parameters(), lr=learning_rate)
train_loss    = 0.0
val_loss      = 0.0
total         = 0.0
num_correct   = 0.0
train_out     = torch.zeros(size=(num_epochs*len(train_dataloader), 2))
val_out       = torch.zeros(size=(torch.ceil(torch.mul(num_epochs*len(train_dataloader),0.002)).type(torch.int32), 2))
val_step      = 0
for t in range(num_epochs):
  for idx, (x, y) in enumerate(train_dataloader, 0):
    x, y    = x.to(device), y.to(device)

    optimizer.zero_grad()      
    y_pred  = model(x)
    loss    = criterion(y_pred, y)
    loss.backward()

    total               += y.size(0)
    train_loss          += loss.item()*y.size(0)
    num_correct         += (torch.argmax(y_pred, dim=1) == y).sum().item()

    train_out[step,0]   = train_loss/total
    train_out[step,1]   = (1-num_correct/total)*100

    if step % 500 == 0:
      with torch.no_grad():
        val_loss            = 0.0
        total_val           = 0.0
        num_correct_val     = 0.0
        for idx, (x, y) in enumerate(val_dataloader, 0):
          x, y                  = x.to(device), y.to(device)
          y_pred                = model(x)
          loss                  = criterion(y_pred, y)          
          val_loss              += loss.item()*y.size(0)
          num_correct_val       += (torch.argmax(y_pred, dim=1) == y).sum().item()
          
          total_val             += y.size(0)
          val_out[val_step,0]   = val_loss/total_val
          val_out[val_step,1]   = (1-num_correct_val/total_val)*100

        print('No.:', step, 
                      ' Training Loss:', train_out[step,0].item(), ' Training Err:', train_out[step,1].item(), 
                      ' Validation Loss:', val_out[val_step,0].item(), ' Validation Err:', val_out[val_step,1].item())
        val_step               += 1

    optimizer.step()

    step    += 1
```    
---

In this example, we obtained training and validation errors of $9.74\%$ and $7.43\%$, which is typical of the performance of a 1-layer NN model. There exists more sophisticated models such as convolutional neural networks that achieve errors of less than $1\%$. Apart from recognizing handwritten digits, ML has also been deployed in several applications in computer vision and natural language processing.



  