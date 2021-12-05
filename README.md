# Instalation Guide
Make a read me file from all installation that maybe was needed in the future

## How to install Nvidia RTX 2060 library and DUDA 11.5

In this section we wiil be install latest driver version of the NVIDIA I mean NVIDIA 495 on Ubuntu 20.04 LTS and also install CUDA 11.5.0,  and libcudnn 8.0.4.

I don't recommend installing the NVIDIA drivers that come with CUDA as they do not contain the dkms drivers that carry over into new kernel upgrades.
The Ubuntu repositories now contain the same drivers as the ```graphics-drivers``` PPA. 
Enter ```apt search nvidia-driver``` To get the latest version of the driver.
In this time the latest version is 495.44.So feel free to install the 495.44 drivers.
```sudo apt install nvidia-driver-495```
