# Instalation Guide
Make a read me file from all installation that maybe was needed in the future

## How to install Nvidia RTX 2060 library and DUDA 11.5

In this section, we will install the latest driver version of the NVIDIA (I mean NVIDIA 495) on Ubuntu 20.04 LTS and also install CUDA 11.5.0,  and libcudnn 8.0.4.

I don't recommend installing the NVIDIA drivers that come with CUDA as they do not contain the dkms drivers that carry over into new kernel upgrades.
The Ubuntu repositories now contain the same drivers as the ```graphics-drivers``` PPA. 
Enter ```apt search nvidia-driver``` To get the latest version of the driver.
In this time the latest version is 495.44.So feel free to install the 495.44 drivers.
Here is how to list all nvidia driver version on your Ubuntu machine using the combination of the apt-cache command and egrep command/grep command:

NOTE: for cuda11.8 you should install Driver 520.0 atleast. 

```apt-cache search 'nvidia-driver-' | grep '^nvidia-driver-[[:digit:]]*' ```

```sudo apt install nvidia-driver-495```

>Another way to install the NVIDIA driver is from *Software & Updates --> Additional Drivers*.

Reboot the system so the new driver takes effect.

Please select the release you want from the list below, and be sure to check www.nvidia.com/drivers for more recent production drivers appropriate for your hardware configuration.
https://developer.nvidia.com/cuda-toolkit-archive

To determine the OS architecture run:

``` uname -m ```

To check your Ubuntu version run:

```lsb_release -a```
Now, download the CUDA 11.5.0 .run file from NVIDIA:

```wget https://developer.download.nvidia.com/compute/cuda/11.5.0/local_installers/cuda_11.5.0_495.29.05_linux.run```

Run the `.run` file as `sudo`:

`sudo sh ./cuda_11.5.0_495.29.05_linux.run`

If you get the following, just choose `Continue`:

```┌──────────────────────────────────────────────────────────────────────────────┐
│ Existing package manager installation of the driver found. It is strongly    │
│ recommended that you remove this before continuing.                          │
│ Abort                                                                        │
│ Continue                                                                     │
│                                                                             
```
Accept the EULA:

```┌──────────────────────────────────────────────────────────────────────────────┐
│  End User License Agreement                                                  │
│  --------------------------                                                  │
│                                                                              │
│  NVIDIA Software License Agreement and CUDA Supplement to                    │
│  Software License Agreement. Last updated: October 8, 2021                   │
│                                                                              │
│  The CUDA Toolkit End User License Agreement applies to the                  │
│  NVIDIA CUDA Toolkit, the NVIDIA CUDA Samples, the NVIDIA                    │
│  Display Driver, NVIDIA Nsight tools (Visual Studio Edition),                │
│  and the associated documentation on CUDA APIs, programming                  │
│  model and development tools. If you do not agree with the                   │
│  terms and conditions of the license agreement, then do not                  │
│  download or use the software.                                               │
│                                                                              │
│  Last updated: October 8, 2021.                                              │
│                                                                              │
│                                                                              │
│  Preface                                                                     │
│  -------                                                                     │
│                                                                              │
│──────────────────────────────────────────────────────────────────────────────│
│ Do you accept the above EULA? (accept/decline/quit):                         │
│ accept
```


Unselect the video driver by pressing the spacebar while `[X] Driver` is highlighted:


```┌──────────────────────────────────────────────────────────────────────────────┐
│ CUDA Installer                                                               │
│ - [ ] Driver                                                                 │
│      [ ] 495.29.05                                                           │
│ + [X] CUDA Toolkit 11.5                                                      │
│   [X] CUDA Samples 11.5                                                      │
│   [X] CUDA Demo Suite 11.5                                                   │
│   [X] CUDA Documentation 11.5                                                │
│   Options                                                                    │
│   Install                                                                    │
│                                                                              │
│                                                                              │
│                                                                              │
│                                                                              │
│                                                                              │
│                                                                              │
│                                                                              │
│                                                                              │
│                                                                              │
│                                                                              │
│                                                                              │
│                                                                              │
│                                                                              │
│ Up/Down: Move | Left/Right: Expand | 'Enter': Select | 'A': Advanced options │
```


Then press the down arrow to `Install`. Press `Enter` then wait for installation to complete.

After the installation is complete add the following to the bottom of your `~/.profile` or add it to the `/etc/profile.d/cuda.sh` file which you might have to create for all users (global):


```# set PATH for cuda 11.5 installation
if [ -d "/usr/local/cuda-11.5/bin/" ]; then
    export PATH=/usr/local/cuda-11.5/bin${PATH:+:${PATH}}
    export LD_LIBRARY_PATH=/usr/local/cuda-11.5/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}
fi
```


## Install libcudnn8

Add the Repo:

**NOTE:** *The 20.04 repo from NVIDIA does not supply libcudnn but the 18.04 repo does and installs just fine into 20.04.*

`echo "deb http://developer.download.nvidia.com/compute/machine-learning/repos/ubuntu1804/x86_64 /" | sudo tee /etc/apt/sources.list.d/cuda_learn.list`


Install the key:

`sudo apt-key adv --fetch-keys  http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/7fa2af80.pub`

Update the system:

`sudo apt update`

Install libcudnn 8.0.4:

`sudo apt install libcudnn8`

I recommend now to **reboot** the system for the changes to take effect.

After it reboots check the installations:

```~$ nvidia-smi
Thu Nov 18 07:31:31 2021       
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 495.44       Driver Version: 495.44       CUDA Version: 11.5     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|                               |                      |               MIG M. |
|===============================+======================+======================|
|   0  NVIDIA GeForce ...  Off  | 00000000:01:00.0  On |                  N/A |
| 40%   38C    P8     1W /  38W |    310MiB /  2000MiB |      4%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+
                                                                               
+-----------------------------------------------------------------------------+
| Processes:                                                                  |
|  GPU   GI   CI        PID   Type   Process name                  GPU Memory |
|        ID   ID                                                   Usage      |
|=============================================================================|
|    0   N/A  N/A      2091      G   /usr/lib/xorg/Xorg                 46MiB |
|    0   N/A  N/A      2680      G   /usr/lib/xorg/Xorg                163MiB |
|    0   N/A  N/A      2906      G   compton                             1MiB |
|    0   N/A  N/A      3262      G   /opt/waterfox/waterfox             85MiB |
+-----------------------------------------------------------------------------+
```
**NOTE:** maybe after installation of the NVIDIA drivers after inserting `nvidia-smi` this error occurred: *NVIDIA-SMI has failed because it couldn't communicate with the NVIDIA driver. Make sure that the latest NVIDIA driver is installed and running.* In this case maybe your Secure Boot is Enable so reboot the PC and press the appropriate key to go to BIOS. after that, change the status of Secure Boot to disable.

and check CUDA install:

```~$ nvcc -V
nvcc: NVIDIA (R) Cuda compiler driver
Copyright (c) 2005-2021 NVIDIA Corporation
Built on Mon_Sep_13_19:13:29_PDT_2021
Cuda compilation tools, release 11.5, V11.5.50
Build cuda_11.5.r11.5/compiler.30411180_0
```

and check libcudnn install:

```~$ /sbin/ldconfig -N -v $(sed 's/:/ /' <<< $LD_LIBRARY_PATH) 2>/dev/null | grep libcudnn
    libcudnn_cnn_infer.so.8 -> libcudnn_cnn_infer.so.8.0.4
    libcudnn.so.8 -> libcudnn.so.8.0.4
    libcudnn_adv_train.so.8 -> libcudnn_adv_train.so.8.0.4
    libcudnn_ops_infer.so.8 -> libcudnn_ops_infer.so.8.0.4
    libcudnn_cnn_train.so.8 -> libcudnn_cnn_train.so.8.0.4
    libcudnn_adv_infer.so.8 -> libcudnn_adv_infer.so.8.0.4
    libcudnn_ops_train.so.8 -> libcudnn_ops_train.so.8.0.4
```



