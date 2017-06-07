
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
(y)es/(n)o/(q)uit [ default is no ]: y

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

### Set PATH
```sh
vi ~/.bashrc
```
```sh
### CUDA PATH
export CUDA_HOME=/usr/local/cuda-8.0
export PATH=/usr/local/cuda-8.0/bin${PATH:+:${PATH}}
export LD_LIBRARY_PATH=/usr/local/cuda-8.0/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}

```

### Check `cuda` working

```sh
nvcc --version
```
```sh
nvcc: NVIDIA (R) Cuda compiler driver
Copyright (c) 2005-2016 NVIDIA Corporation
Built on Tue_Jan_10_13:22:03_CST_2017
Cuda compilation tools, release 8.0, V8.0.61

```
### Test`cuda`


#### Install samples if you didn't install the CUDA 8.0 Samples
```sh
cuda-install-samples-8.0.sh ~/
```

or

```sh
cd ~/NVIDIA_CUDA-8.0_Samples/1_Utilities/bandwidthTest/
make 
```
```sh
"/usr/local/cuda-8.0"/bin/nvcc -ccbin g++ -I../../common/inc  -m64    -gencode arch=compute_20,code=sm_20 -gencode arch=compute_30,code=sm_30 -gencode arch=compute_35,code=sm_35 -gencode arch=compute_37,code=sm_37 -gencode arch=compute_50,code=sm_50 -gencode arch=compute_52,code=sm_52 -gencode arch=compute_60,code=sm_60 -gencode arch=compute_60,code=compute_60 -o bandwidthTest.o -c bandwidthTest.cu
nvcc warning : The 'compute_20', 'sm_20', and 'sm_21' architectures are deprecated, and may be removed in a future release (Use -Wno-deprecated-gpu-targets to suppress warning).
"/usr/local/cuda-8.0"/bin/nvcc -ccbin g++   -m64      -gencode arch=compute_20,code=sm_20 -gencode arch=compute_30,code=sm_30 -gencode arch=compute_35,code=sm_35 -gencode arch=compute_37,code=sm_37 -gencode arch=compute_50,code=sm_50 -gencode arch=compute_52,code=sm_52 -gencode arch=compute_60,code=sm_60 -gencode arch=compute_60,code=compute_60 -o bandwidthTest bandwidthTest.o 
nvcc warning : The 'compute_20', 'sm_20', and 'sm_21' architectures are deprecated, and may be removed in a future release (Use -Wno-deprecated-gpu-targets to suppress warning).
mkdir -p ../../bin/x86_64/linux/release
cp bandwidthTest ../../bin/x86_64/linux/release

```

#### Run Samples

```sh
./bandwidthTest
```
```
[CUDA Bandwidth Test] - Starting...
Running on...

 Device 0: GeForce GTX 1070
 Quick Mode

 Host to Device Bandwidth, 1 Device(s)
 PINNED Memory Transfers
   Transfer Size (Bytes)	Bandwidth(MB/s)
   33554432			6343.6

 Device to Host Bandwidth, 1 Device(s)
 PINNED Memory Transfers
   Transfer Size (Bytes)	Bandwidth(MB/s)
   33554432			6441.1

 Device to Device Bandwidth, 1 Device(s)
 PINNED Memory Transfers
   Transfer Size (Bytes)	Bandwidth(MB/s)
   33554432			190413.9

Result = PASS

NOTE: The CUDA Samples are not meant for performance measurements. Results may vary when GPU Boost is enabled.

```

In case of error or problems with the legacy nvidia driver(not `cuda`, reinstall it.


## Install `cuDNN`

Download [here](https://developer.nvidia.com/cudnn)

```sh
tar -zxvf cudnn-8.0-linux-x64-v5.1.tgz
cd cuda
sudo cp include/cudnn.h /usr/local/cuda-8.0/include/
sudo cp lib64/* /usr/local/cuda-8.0/lib64/
sudo chmod a+r /usr/local/cuda-8.0/*

```
