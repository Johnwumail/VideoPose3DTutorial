# Environment Setup
My env
- GPU: Nvidia 1080Ti
- OS: Ubuntu 18.04
VideoPose3D need pytorch installed. I will install following items
- nvidia driver for GPU
- cuda 10.1
- pytorch

## Install nvidia driver
- detect the model of nvidia graphic card and the recommended driver
```
john@john-All-Series:~$ ubuntu-drivers devices
== /sys/devices/pci0000:00/0000:00:02.0/0000:02:00.0 ==
modalias : pci:v000010DEd00001B06sv00001458sd00003760bc03sc00i00
vendor   : NVIDIA Corporation
model    : GP102 [GeForce GTX 1080 Ti]
driver   : nvidia-driver-390 - distro non-free
driver   : nvidia-driver-430 - distro non-free recommended
driver   : xserver-xorg-video-nouveau - distro free builtin
```

- Install the recommanded nvidia driver
```
sudo ubuntu-drivers autoinstall
```

- Reboot and check the driver version with nvidia-smi
```
john@john-All-Series:~$ nvidia-smi
Sun Oct 20 09:55:04 2019       
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 430.26       Driver Version: 430.26       CUDA Version: 10.2     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|===============================+======================+======================|
|   0  GeForce GTX 108...  Off  | 00000000:01:00.0  On |                  N/A |
|  0%   55C    P5    20W / 250W |    186MiB / 11170MiB |      0%      Default |
+-------------------------------+----------------------+----------------------+
|   1  GeForce GTX 108...  Off  | 00000000:02:00.0 Off |                  N/A |
|  0%   38C    P8    10W / 250W |      2MiB / 11178MiB |      0%      Default |
+-------------------------------+----------------------+----------------------+
                                                                               
+-----------------------------------------------------------------------------+
| Processes:                                                       GPU Memory |
|  GPU       PID   Type   Process name                             Usage      |
|=============================================================================|
|    0      1162      G   /usr/lib/xorg/Xorg                           106MiB |
|    0      1410      G   /usr/bin/gnome-shell                          77MiB |
+-----------------------------------------------------------------------------+

```

## Install CUDA
- Verify environment
Go through the https://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html document and verify if the precondition is meet.
Here is the output on my env
```
john@john-All-Series:~$ lspci | grep -i nvidia
01:00.0 VGA compatible controller: NVIDIA Corporation GP102 [GeForce GTX 1080 Ti] (rev a1)
01:00.1 Audio device: NVIDIA Corporation GP102 HDMI Audio Controller (rev a1)
02:00.0 VGA compatible controller: NVIDIA Corporation GP102 [GeForce GTX 1080 Ti] (rev a1)
02:00.1 Audio device: NVIDIA Corporation GP102 HDMI Audio Controller (rev a1)

john@john-All-Series:~$ uname -m && cat /etc/*release
x86_64
DISTRIB_ID=Ubuntu
DISTRIB_RELEASE=18.04
DISTRIB_CODENAME=bionic
DISTRIB_DESCRIPTION="Ubuntu 18.04.3 LTS"
NAME="Ubuntu"
VERSION="18.04.3 LTS (Bionic Beaver)"
ID=ubuntu
ID_LIKE=debian
PRETTY_NAME="Ubuntu 18.04.3 LTS"
VERSION_ID="18.04"
HOME_URL="https://www.ubuntu.com/"
SUPPORT_URL="https://help.ubuntu.com/"
BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"
PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"
VERSION_CODENAME=bionic
UBUNTU_CODENAME=bionic

john@john-All-Series:~$ gcc --version
gcc (Ubuntu 7.4.0-1ubuntu1~18.04.1) 7.4.0
Copyright (C) 2017 Free Software Foundation, Inc.
This is free software; see the source for copying conditions.  There is NO
warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.

john@john-All-Series:~$ sudo apt-get install linux-headers-$(uname -r)
[sudo] password for john: 
Reading package lists... Done
Building dependency tree       
Reading state information... Done
linux-headers-5.0.0-31-generic is already the newest version (5.0.0-31.33~18.04.1).
linux-headers-5.0.0-31-generic set to manually installed.
0 upgraded, 0 newly installed, 0 to remove and 0 not upgraded.

```

- Install CUDA from nvida website
I install the latest version is CUDA Toolkit 10.1 Update 2 

https://developer.nvidia.com/cuda-download

I chose deb local install with following commands (provided in the website)

```
wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/cuda-ubuntu1804.pinsudo 
mv cuda-ubuntu1804.pin /etc/apt/preferences.d/cuda-repository-pin-600
wget http://developer.download.nvidia.com/compute/cuda/10.1/Prod/local_installers/cuda-repo-ubuntu1804-10-1-local-10.1.243-418.87.00_1.0-1_amd64.deb
sudo dpkg -i cuda-repo-ubuntu1804-10-1-local-10.1.243-418.87.00_1.0-1_amd64.deb
sudo apt-key add /var/cuda-repo-10-1-local-10.1.243-418.87.00/7fa2af80.pub
sudo apt-get updatesudo apt-get -y install cuda
```

- Post Install Action - set environment path
I add following lines into ~/.profile
```bash
export PATH=/usr/local/cuda-10.1/bin:/usr/local/cuda-10.1/NsightCompute-2019.1${PATH:+:${PATH}}
export LD_LIBRARY_PATH=/usr/local/cuda-10.1/lib64\
                         ${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}
```

## Install Pytorch
- create & enable virutal env
```bash
# Install python virtual environment
sudo apt-get install python3-venv
# Create virtual environment
python3 -m venv videopose3d_env
# Enbale virtual environment
source videopose3d_env/bin/activate
(videopose3d_env) john@john-All-Series:~/Documents$
```

- Install Pytorch
Visit https://pytorch.org/get-started/locally/ and install by followin selection
  - Stable 1.3
  - Linux
  - pip
  - python 3.6
  - cuda 10.1

Install Pytorch
```bash
pip3 install torch torchvision
```


