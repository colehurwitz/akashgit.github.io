---
layout: post
comments: true
title: "Installing Tensorflow on Dice"
date: 2016-03-29
---

Right, yesterday during one of the reading groups meeting we decided to have the next session on TensorFlow installation on DICE machines.
So I decided to test it out and find why it is considered to be problamatic. 

Turns out its very simple!

I'd recommend that you use VirtualEnv as otherwise you'd need `sudo` access to the machine.

Right so here are the steps for installing the GPU version:

1. Activate your VirtualEnv
2. `pip install --upgrade https://storage.googleapis.com/tensorflow/linux/gpu/tensorflow-0.7.1-cp27-none-linux_x86_64.whl`
3. Check the version of `cuda` on your machine. On DICE its in the `/opt` directory.
4. `export PATH=$PATH:"/opt/cuda-X.X.XX/bin"` where its cuda-7.5.18 for my machine
5. `export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:"/opt/cuda-x.x.xx/lib64"`

Equivalently you can append these things to your config file.

Thats it!! You are good to go.

