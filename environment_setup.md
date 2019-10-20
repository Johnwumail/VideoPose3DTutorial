# Environment Setup
GPU: Nvidia 1080Ti
OS: Ubuntu 18.04

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
