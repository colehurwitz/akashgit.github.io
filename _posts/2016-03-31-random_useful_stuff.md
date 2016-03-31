---
layout: post
title: "Random Useful Stuff"
date: 2016-03-31
---

### Some CUDA related commands I frequently forget:
1. `CUDA_VISIBLE_DEVICES=1 python program.py`
2. `nvidia-smi`

### Starting notebook in specific browser (because SL7 is complete mess to work with sometimes)
3. `nice ipython notebook --browser=firefox`

### Befor the advent of the AUTODIFF:
4. Derivative of the KL Divergence between two exponential family distributions $$ q(x|\alpha) $$ and $$ p(x| \beta) $$ : 
    $$(\alpha - \beta)^TI(\alpha)$$
5. Here $$ I(\alpha) $$ is the Fisher Information, which is also the second derivative of the log normalizer in case of exponential family. 

### Sometimes my machine decides to not read my rc file and so I need to export these munually:
6. `export LD_LIBRARY_PATH=/lib64:/lib:~/atlas:/opt/cuda-7.5.18/lib64:$LD_LIBRARY_PATH`
7. `export ATLAS=~/atlas/libatlas.so`
