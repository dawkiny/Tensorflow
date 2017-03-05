# Tensorflow

## Install `cuda`


### Verify `gcc` installed

```sh
gcc --version
```
```sh
gcc (Ubuntu 5.4.0-6ubuntu1~16.04.4) 5.4.0 20160609
Copyright (C) 2015 Free Software Foundation, Inc.
This is free software; see the source for copying conditions.  There is NO
warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
```

## Install `nvidia` Drivers

## Install `cuda`

### Download `cuda runfile`

Download it [here](https://developer.nvidia.com/cuda-downloads)

### Exit `X server` if it is running

1. `logout` or `reboot`
2. enter `tty`
3. `stop service`
```sh
sudo service lightdm stop
sudo init 3 (or sudo init 5)
```

### Run `cuda runfile`
```sh
sudo bash cuda_8.0.61_375.26_linux.run
```
```sh
...
6. NVIDIA CUDA General Terms
----------------------------

The Software, on the Windows platform, may collect
non-personally identifiable information for the purposes of
customizing information delivered to you and improving future
versions of the Software. Such information, including IP
address and system configuration, will only be collected on an
anonymous basis and cannot be linked to any personally
identifiable information. Personally identifiable information
such as your username or hostname is not collected.

-------------------------------------------------------------
Do you accept the previously read EULA?
accept/decline/quit: accept  

Install NVIDIA Accelerated Graphics Driver for Linux-x86_64 375.26?
(y)es/(n)o/(q)uit: y

Do you want to install the OpenGL libraries?
(y)es/(n)o/(q)uit [ default is yes ]: y

Do you want to run nvidia-xconfig?
This will update the system X configuration file so that the NVIDIA X driver
is used. The pre-existing X configuration file will be backed up.
This option should not be used on systems that require a custom
X configuration, such as systems with multiple GPU vendors.
(y)es/(n)o/(q)uit [ default is no ]: n

Install the CUDA 8.0 Toolkit?
(y)es/(n)o/(q)uit: y

Enter Toolkit Location
 [ default is /usr/local/cuda-8.0 ]:  

Do you want to install a symbolic link at /usr/local/cuda?
(y)es/(n)o/(q)uit: y

Install the CUDA 8.0 Samples?
(y)es/(n)o/(q)uit: y

Enter CUDA Samples Location
 [ default is /home/pydemia ]: 

Installing the NVIDIA display driver...

```


## Install `tensorflow`
```sh
conda create -n tensorflow python=3.5
```
## Usage
* [Basics on Tensorflow](https://github.com/dawkiny/Tensorflow/blob/master/scripts/basic.md)
