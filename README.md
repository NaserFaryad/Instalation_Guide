# Instalation Guide
Make a read me file from all installation that maybe was needed in the future

## How to install Nvidia RTX 2060 library and DUDA 11.5

In this section, we will install the latest driver version of the NVIDIA (I mean NVIDIA 495) on Ubuntu 20.04 LTS and also install CUDA 11.5.0,  and libcudnn 8.0.4.

I don't recommend installing the NVIDIA drivers that come with CUDA as they do not contain the dkms drivers that carry over into new kernel upgrades.
The Ubuntu repositories now contain the same drivers as the ```graphics-drivers``` PPA. 
Enter ```apt search nvidia-driver``` To get the latest version of the driver.
In this time the latest version is 495.44.So feel free to install the 495.44 drivers.

```sudo apt install nvidia-driver-495```

>Another way to install the NVIDIA driver is from *Software & Updates --> Additional Drivers*.

Reboot the system so the new driver takes effect.
Now, download the CUDA 11.5.0 .run file from NVIDIA:

```wget https://developer.download.nvidia.com/compute/cuda/11.5.0/local_installers/cuda_11.5.0_495.29.05_linux.run```

Run the `.run` file as `sudo`:

`sudo sh ./cuda_11.5.0_495.29.05_linux.run`

If you get the following, just choose `Continue`:

`┌──────────────────────────────────────────────────────────────────────────────┐
│ Existing package manager installation of the driver found. It is strongly    │
│ recommended that you remove this before continuing.                          │
│ Abort                                                                        │
│ Continue                                                                     │
│                                                                             
`
Accept the EULA:

`┌──────────────────────────────────────────────────────────────────────────────┐
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
│ accept`                                                                       

Unselect the video driver by pressing the spacebar while `[X] Driver` is highlighted:

`┌──────────────────────────────────────────────────────────────────────────────┐
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
│ Up/Down: Move | Left/Right: Expand | 'Enter': Select | 'A': Advanced options │`

Then press the down arrow to `Install`. Press `Enter` then wait for installation to complete.

After the installation is complete add the following to the bottom of your `~/.profile` or add it to the `/etc/profile.d/cuda.sh` file which you might have to create for all users (global):

`# set PATH for cuda 11.5 installation
if [ -d "/usr/local/cuda-11.5/bin/" ]; then
    export PATH=/usr/local/cuda-11.5/bin${PATH:+:${PATH}}
    export LD_LIBRARY_PATH=/usr/local/cuda-11.5/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}
fi`

