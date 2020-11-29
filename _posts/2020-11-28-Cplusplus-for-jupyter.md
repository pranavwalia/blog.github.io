---
layout: post
title: C++ For Jupyter Notebook
categories: [Computer Science,C++]
tags: [C++]
description: Today I will show you how to get an interactive computing environment for C++ working with Jupyter Notebook.
permalink: cplusplus-for-jupyter
fullview: false
usemathjax: true
comments: false

---

When I'm experimenting with models I typically prefer to have my math and code in the same place. Python is the language of choice for data scientists as it integrates seamlessly with [Jupyter Notebook](https://jupyter.org/) allowing for carefully placed analysis and explanations alongside code modules. However, recently I've been working on integrating a model into a piece of software where low latency is vital. C++ was the obvious answer in terms of language choice. I began looking for an interactive computing solution in C++ and eventually came across [Xeus](https://github.com/jupyter-xeus/xeus); a C++ kernel for [Jupyter Notebook](https://jupyter.org/) and [Xeus-Cling](https://github.com/jupyter-xeus/xeus-cling); a C++ interpreter. Together, these two frameworks allow for seamless interactive computing.

## Requirements:

* Mac OS/Linux/(Windows is still experimental at the time of this article)
* Conda package manager

## Step 1: Install Conda 

* Download the [conda](https://www.anaconda.com/products/individual) package manager and install the appropriate version for your operating system



## Step 2: Setup

Before you install the modules, you want to set up your own environment to prevent conflicts with your default setup. Open up a terminal and type 'conda activate'. Enter the following commands

```bash
conda create -n cling
```

Next, you want to install cling to your particular environment.

```bash
conda install xeus-cling -c conda-forge
```

Finally, install Xeus:

```bash
conda install xeus -c conda-forge
```



## Step 3: Open A Notebook

Open a shell and switch to your cling environment.

```bash
conda activate cling
```

Open a notebook

```bash
jupyter notebook
```

You should now see the option to create a C++ notebook in Jupyter.

![xeus-cling](/assets/images/xeus-cling.png)