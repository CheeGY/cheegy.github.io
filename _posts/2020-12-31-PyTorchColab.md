---
layout: post
title: "Recognizing Handwritten Digits using Machine Learning - PyTorch and Colab"
author: "Kong Yao"
categories: journal
tags: [machine learning]
image: post4.jpg
---
One of the most explored applications in the field of machine learning (ML) is the recognition of handwritten digits from low-resolution images. In this note, we provide a basic PyTorch implementation that is compatible with Google Colab. Due to its simplicity, it is suitable for anyone who may be interested to get started with PyTorch and Colab.

In this example, we use the famous MNIST (Modified National Institute of Standards and Technology) dataset, which is the de facto "Hello World" dataset for computer vision. It contains images of handwritten digits ($0$ to $9$) and below are some samples of the images in the dataset,

![alt text](/assets/img/sample_mnist.PNG "MNIST samples")

Observe that some of these digits can be quite ambiguous, and may even be difficult for humans to recognize. With machine learning, the objective is to construct a computational model that recognizes these digits automatically and with high accuracy.

To achieve this, the first step is to construct and train the ML model, using one part of the dataset. This training process allows the model to **learn** important patterns, also known as features, found in these images. This first part of the dataset is often called the *training dataset*. 

Next, using what it has learned in the training process, the model attempts to **predict** the digits in the images of the other part of the dataset, also known as the *validation dataset*.

Before going into the details of the code implementation, let's briefly introduce PyTorch and Google Colab.

---

## What is PyTorch?

![alt text](/assets/img/torch_logo.png "Pytorch")

[PyTorch](https://pytorch.org/) is a machine learning/deep learning open source library, based on the programming language, Python. It provides two key features; tensor computing through GPUs, as well as neural networks based on an automatic differentiation system. What makes PyTorch popular among data scientists and AI enthusiasts is its ability to parallelize computations using GPUs, and that speeds up training and data processing significantly.


---

## What is Google Colab?

![alt text](/assets/img/colab_logo.png "Google Colab")

[Google Colab](https://colab.research.google.com/) is an web-based application that allows you to write and execute Python, right from your browser. Colab has several libraries pre-installed, including PyTorch. This allows users with Google accounts to use PyTorch and many machine learning libraries in Colab immediately, without any further installation.

---

## Pre-processing of the MNIST Dataset
Before construction and training of the model, data pre-processing is often necessary to extract and partition the training and validation datasets, and to normalize the samples in the dataset. The following code snippet performs this pre-processing step, after importing the relevant libraries. 

```python
# Import PyTorch libraries
import torch
import torch.nn as nn
import torch.optim as optim
import torchvision as thv
from torch.utils.data import DataLoader, TensorDataset

device  = torch.device("cuda:0" if torch.cuda.is_available() else "cpu")

# Load the MNIST dataset from torchvision
train   = thv.datasets.MNIST('./', download=True, train=True)
val     = thv.datasets.MNIST('./', download=True, train=False)

# Reshape training and validation features from (batch_size,28,28) to (batch_size,28*28) and attach to GPU
xtrain  = train.data.view(-1, 28*28).to(device)
xval    = val.data.view(-1, 28*28).to(device)

# Normalize training and validation features from [0,255] to [0,1] 
xtrain  = xtrain/255.0
xval    = xval/255.0

# Attach training and validation labels to GPU
ytrain  = train.targets.to(device)
yval    = val.targets.to(device)

# Set training and validation dataloaders 
train_dataset   = TensorDataset(xtrain, ytrain)
train_dataloader= DataLoader(train_dataset, batch_size=32, shuffle=True)

val_dataset     = TensorDataset(xval, yval)
val_dataloader  = DataLoader(val_dataset, batch_size=32,shuffle=False)
```

Another convenient aspect about Colab and PyTorch is that any code snippet can be copied or extracted directly into a Jupyter notebook embedded in Colab and can be executed immediately. For a better understanding, try it out yourself in [Colab](https://colab.research.google.com/).

----

## Model Construction
Next, a simple 1-layer linear neural network is constructed and serves as the model. It uses ReLU activation functions and the *torch.nn.Sequential* module in PyTorch. Documentation for these functions can be found [here](https://pytorch.org/docs/stable/generated/torch.nn.ReLU.html) and [here](https://pytorch.org/docs/stable/generated/torch.nn.Sequential.html).

```python
D_in, D_out = 784, 10
model       = torch.nn.Sequential(
                torch.nn.Linear(D_in, D_out),
                torch.nn.ReLU(),
                ).to(device)
```

---

## Model Training and Validation (prediction)
The following module is then implemented to train the model so that it learns patterns/features in the given images. Since this is a multi-class classification problem, the [cross entropy loss](https://pytorch.org/docs/stable/generated/torch.nn.CrossEntropyLoss.html) is used as the objective function. [Stochastic gradient descent](https://pytorch.org/docs/stable/optim.html?highlight=sgd%20optim#torch.optim.SGD) (SGD) is used as the optimizer. 

```python
num_epochs      = 25
learning_rate   = 0.08
criterion       = nn.CrossEntropyLoss()
optimizer       = torch.optim.SGD(model.parameters(), lr=learning_rate)
train_loss      = 0.0
val_loss        = 0.0
total           = 0.0
num_correct     = 0.0
train_out       = torch.zeros(size=(num_epochs*len(train_dataloader), 2))
val_out         = torch.zeros(size=(torch.ceil(torch.mul(num_epochs*len(train_dataloader),0.002)).type(torch.int32), 2))
val_step        = 0
for t in range(num_epochs):
  for idx, (x, y) in enumerate(train_dataloader, 0):
    x, y    = x.to(device), y.to(device)

    optimizer.zero_grad()      
    y_pred  = model(x)
    loss    = criterion(y_pred, y)
    loss.backward()

    total       += y.size(0)
    train_loss  += loss.item()*y.size(0)
    num_correct += (torch.argmax(y_pred, dim=1) == y).sum().item()

    train_out[step,0] = train_loss/total
    train_out[step,1] = (1-num_correct/total)*100

    if step % 500 == 0:
      with torch.no_grad():
        val_loss        = 0.0
        total_val       = 0.0
        num_correct_val = 0.0
        for idx, (x, y) in enumerate(val_dataloader, 0):
          x, y              = x.to(device), y.to(device)
          y_pred            = model(x)
          loss              = criterion(y_pred, y)          
          val_loss          += loss.item()*y.size(0)
          num_correct_val   += (torch.argmax(y_pred, dim=1) == y).sum().item()
          
          total_val         += y.size(0)
          val_out[val_step,0] = val_loss/total_val
          val_out[val_step,1] = (1-num_correct_val/total_val)*100

        print('No.:', step, 
              ' Training Loss:', train_out[step,0].item(),
              ' Training Err:', train_out[step,1].item(), 
              ' Validation Loss:', val_out[val_step,0].item(), 
              ' Validation Err:', val_out[val_step,1].item())
        val_step            += 1

    optimizer.step()

    step    += 1
```    
---

## Results and Conclusion

![alt text](/assets/img/post4_train_valid_error.PNG "Training and Validation errors")

In this example, training and validation errors of $9.74\%$ and $7.43\%$ are attained, after training for 25 epochs. These results are typical of the performance of a 1-layer NN model for the MNIST dataset. There exist more complex models such as convolutional neural networks that can achieve errors of less than $1\%$. Apart from recognizing handwritten digits, ML has also been deployed in several applications in computer vision and natural language processing.



  