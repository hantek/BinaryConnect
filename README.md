# Neural Networks with Few Multiplications

This repository contains necessary codes to reproduce the experimental results
reported in the paper
[Neural Networks with Few Multiplications](http://arxiv.org/abs/1510.03009).
It is forked from Matthieu Courbariaux's
[BinaryConnect](https://github.com/MatthieuCourbariaux/BinaryConnect) repo.

The 3 differnt branches in this repo corresponds to 3 different network configurations.
They are:

* **binary**: Implements binary connect with quantized backprop.
* **ternary**: Implements ternary connect with quantized backprop.
* **fullresolution**: A control group training with ordinary backprop and no weight binarization.

You can use 

    git checkout <branch name>

to switch between them.

All the three branches provide scripts for MNIST, CIFAR-10, and SVHN datasets.
To run those scripts, you can use the same command no matter which branch you
are in. Execute the following commands for different datasets:

## MNIST

    python mnist.py
    
This python script trains an MLP on MNIST. It should run for less than 1 hour
on a Tesla M2050 GPU. The final test error should be around 1.33%
(fullresolution branch), 1.29% (binary branch), and 1.15% (ternarybranch).

## CIFAR-10

    python cifar10.py
    
This python script trains a CNN on CIFAR-10. It should run for about 5 hours
on a Titan X GPU. The final test error should be around 15.64% (fullresolution),
12.08% (binary), and 12.01% (ternary).

## SVHN
    
    export SVHN_LOCAL_PATH=/tmp/SVHN/
    python svhn_preprocessing.py
    
This python script (taken from Pylearn2) computes a preprocessed version of the
SVHN dataset in a temporary folder.

    python svhn.py
    
This python script trains a CNN on SVHN. It should run for about 15 hours on a
Titan X GPU. The final test error should be around 2.85% (fullresolution),
2.48% (binary), and 2.42% (ternary).

## Requirements

* Python, Numpy, Scipy
* Theano 0.6 or later
* Pylearn2 0.1
* PyTables (only for the SVHN dataset)
* a fast GPU or a large amount of patience

## More advanced:
The python scripts mnist.py, cifar10.py and svhn.py contain all the relevant
hyperparameters. It is very straightforward to modify them. layer.py contains
the binarization function (binarize_weights) and quantized backprop function
(quantized_bprop). 

To conveniently disable quantized backprop alone, go to the model.py file,
comment out line 112 and uncomment line 114.

To monitor the representation at each layer, uncomment line 293~339. You
should be able to see an animated figure showing histograms about each layer's
distribution.

Have fun!

