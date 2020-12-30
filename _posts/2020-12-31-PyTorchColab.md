---
layout: post
title: "Recognizing Handwritten Digits using Tools of Machine Learning"
author: "Kong Yao"
categories: journal
tags: [machine learning]
image: post4.jpg
---
One of the most explored applications in the field of machine learning (ML) is the recognition of handwritten digits from images. In this note, a basic PyTorch implementation of this application is provided. This is compatible with Google Colab and hence, it is suitable for anyone who may be interested to get started with these tools.

For this example, we utilized the famous MNIST database, which contains images of handwritten digits ($0$ to $9$). Here are some samples of these images,

![alt text](/assets/img/sample_mnist.PNG "MNIST samples")

As observed, some of these digits are quite ambiguous, even for humans. With machine learning, the objective is to construct a model that can recognize these digits automatically. Ideally, this should be done with high accuracy and without human supervision. 

Typical of many machine learning applications, the first step is to construct and train the ML model, using part of the database. The training process allows the model to **learn** the patterns/features of these images. This first part of the dataset is often called the *training dataset*. Next, using what it has learnt in the training process, the model attempts to **predict** the digits in the remaining images of the dataset, also called the *validation dataset*.

Before going into the details of the code implementation, let's briefly introduce PyTorch and Google Colab.

---

## What is PyTorch?

![alt text](/assets/img/torch_logo.png "Pytorch")

[PyTorch](https://pytorch.org/) is a machine learning/deep learning open source library, based on the programming language, Python. It provides two key features; tensor computing through GPUs, as well as neural networks based on an automatic differentiation system.

What makes PyTorch popular among data scientists and AI enthusiasts is its ability to parallelize computations using GPUs, and this speeds things up significantly.

## What is Google Colab?

![alt text](/assets/img/colab_logo.png "Google Colab")

[Google Colab](https://colab.research.google.com/) is an web-based application that allows you to write and execute Python, right from your browser. Colab has several libraries pre-installed, including PyTorch. This allows users with Google accounts to use PyTorch in Colab immediately, without any further installation.

---

## Pre-processing of the database
Before construction and training of the ML model, pre-processing is often necessary to extract and partition the training and validation datasets and to normalize the samples in the database. The following code snippet performs this pre-processing, after importing the relevant libraries. 

```Python3
# Import PyTorch libraries
import torch
import torch.nn as nn
import torch.optim as optim
import torchvision as thv
from torch.utils.data import DataLoader, TensorDataset

device = torch.device("cuda:0" if torch.cuda.is_available() else "cpu")

# Load the MNIST dataset from torchvision
train = thv.datasets.MNIST('./', download=True, train=True)
val = thv.datasets.MNIST('./', download=True, train=False)

# Reshape training and validation features from (batch_size,28,28) to (batch_size,28*28) and attach to GPU
xtrain = train.data.view(-1, 28*28).to(device)
xval = val.data.view(-1, 28*28).to(device)

# Normalize training and validation features from [0,255] to [0,1] 
xtrain = xtrain/255.0
xval = xval/255.0

# Attach training and validation labels to GPU
ytrain = train.targets.to(device)
yval = val.targets.to(device)

# Set training and validation dataloaders 
train_dataset = TensorDataset(xtrain, ytrain)
train_dataloader = DataLoader(train_dataset, batch_size=32, shuffle=True)

val_dataset = TensorDataset(xval, yval)
val_dataloader = DataLoader(val_dataset, batch_size=32,shuffle=False)
```

Another convenient thing about Colab and PyTorch is that this snippet above can be extracted directly into a Jupyter notebook of Colab and can be executed immediately.

----

## Model construction
Next, we construct a 1-layer linear neural network as our model, using ReLU activation functions and the Sequential nn module in PyTorch.

```Python3
D_in, D_out = 784, 10
model = torch.nn.Sequential(
    torch.nn.Linear(D_in, D_out),
    torch.nn.ReLU(),
).to(device)
```

---

## Model training and validation (prediction)
Following that, we implement the following training module, where the model is being trained. Since we are dealing with a multi-class classification problem, the cross entropy loss is used as the objective function and stochastic gradient descent (SGD) is used as the optimizer. 

```Python3
num_epochs = 15
learning_rate = 0.08
criterion = nn.CrossEntropyLoss()
optimizer = torch.optim.SGD(model.parameters(), lr=learning_rate)
train_loss = 0.0
val_loss = 0.0
total = 0.0
num_correct = 0.0
train_out = torch.zeros(size=(num_epochs*len(train_dataloader), 2))
val_out = torch.zeros(size=(torch.ceil(torch.mul(num_epochs*len(train_dataloader),0.002)).type(torch.int32), 2))
val_step = 0
for t in range(num_epochs):
  for idx, (x, y) in enumerate(train_dataloader, 0):
    x, y = x.to(device), y.to(device)

    optimizer.zero_grad()      
    y_pred = model(x)
    loss = criterion(y_pred, y)
    loss.backward()

    total += y.size(0)
    train_loss += loss.item()*y.size(0)
    num_correct += (torch.argmax(y_pred, dim=1) == y).sum().item()

    train_out[step,0] = train_loss/total
    train_out[step,1] = (1-num_correct/total)*100

    if step % 500 == 0:
      with torch.no_grad():
        val_loss = 0.0
        total_val = 0.0
        num_correct_val = 0.0
        for idx, (x, y) in enumerate(val_dataloader, 0):
          x, y = x.to(device), y.to(device)
          y_pred = model(x)
          loss = criterion(y_pred, y)          
          val_loss += loss.item()*y.size(0)
          num_correct_val += (torch.argmax(y_pred, dim=1) == y).sum().item()
          
          total_val += y.size(0)
          val_out[val_step,0] = val_loss/total_val
          val_out[val_step,1] = (1-num_correct_val/total_val)*100

        print('No.:', step, 
              ' Training Loss:', train_out[step,0].item(),
              ' Training Err:', train_out[step,1].item(), 
              ' Validation Loss:', val_out[val_step,0].item(), 
              ' Validation Err:', val_out[val_step,1].item())
        val_step               += 1

    optimizer.step()

    step    += 1
```    
---

## Results and Conclusion
In this example, we obtained training and validation errors of $9.74\%$ and $7.43\%$, which is typical of the performance of a 1-layer NN model for the MNIST database. There exists more sophisticated models such as convolutional neural networks that can achieve errors of less than $1\%$. Apart from recognizing handwritten digits, ML has also been deployed in several applications in computer vision and natural language processing.



  