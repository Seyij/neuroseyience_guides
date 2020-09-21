# Easy GPU environment installation for Deeplabcut - Guide
By Oluwaseyi Jesusanmi - University of Dundee  
Twitter: @neuroseyience

---

Hello! This guide will show you how to install [deeplabcut](https://github.com/DeepLabCut/DeepLabCut) for use with a gpu with just a few lines of conda code.

Optionally I also include instructions for installation on any Directx12 GPU using  [tensorflow-directml](https://github.com/microsoft/tensorflow-directml). Useful for those on AMD or Intel graphics cards.


This guide is for windows 10 using [Anaconda](https://www.anaconda.com/products/individual), using conda for environment management. The program I use to work with conda is anaconda prompt but other programs can be used. By the end you should have a functioning conda environment which works with your GPU and Deeplabcut. Deeplabcut version is 2.1.8.2.

For more help with environmet management with conda, I find this [conda cheat sheet](https://kapeli.com/cheat_sheets/Conda.docset/Contents/Resources/Documents/index) very helpful.

---

#### Make a Tensorflow-GPU Environment

Open Anaconda prompt and type in the following on a single line. The "dlc_gpu" can be changed to whatever you want the environment to be named.

```dos
conda create -n dlc_gpu python=3.6 cudnn=7.1.4=cuda9.0_0 cuda=9.0 tensorflow-gpu=1.12.0
```

Tensorflow-gpu has very strict dependencies on what package versions it needs to work. The above is a combination that I have found to work.

```dos
conda activate dlc_gpu
conda install -c conda-forge ffmpeg
pip install deeplabcut
pip install -U wxPython==4.0.7.post2
```
Activating the environment allows us to install more packages.
This specific version of wxPython is to avoid errors in the labelling stage (see thread [here](https://github.com/DeepLabCut/DeepLabCut/issues/682)).
Fffmpeg is for some video functions of deeplabcut.

And there, that's it installed! Feel free to start using deeplabcut. If you want to test whether your GPU has been recognised, first open a python window by typing python within your environment. Then do the following:

```python
import tensorflow as tf
sess = tf.Session(config=tf.ConfigProto(log_device_placement=True))

```
This should bring up information about your graphics card.

To open the deeplabcut user interface, open an ipython window by typing ipython in your environment. Then do the following:

```python
import deeplabcut
deeplabcut.launch_dlc()
```
The user interface will then come up. The [deeplabcut github](https://github.com/DeepLabCut/DeepLabCut) has plenty of guides and tutorials for how to use it.

---

#### Make a Tensorflow-Directml environment


[Tensorflow-directml](https://github.com/microsoft/tensorflow-directml) is amazing as it not only makes installation even EASIER, but it allows you to have tensorflow with hardware accelleration ANY modern GPU. That includes AMD, Nvidia, and even Intel!

The caveat is that this is in active development/pre-release. This means the performance may not be as high as Nvidia's CUDA at the momemt, and the codebase is changing. But at least for now, the current version works with deeplabcut. And the directml team are great at responding to help requests.

Anyway here is the code!

```dos
conda create -n dlc_directml python=3.6
conda activaate dlc_directml

pip install tensorflow-directml
pip install deeplabcut
pip install -U wxPython==4.0.7.post2
conda install -c conda-forge ffmpeg
```

Checking your gpu and starting deeplabcut will be the same as the normal tensorflow gpu environment.

---

Thank you for reading my guide! If you have any feedback, I'd like to hear it so I can improve!