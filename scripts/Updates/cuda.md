# Update `cuda` 8 to 9


## Remove the old packages

```sh
sudo apt-get purge 'nvidia-*' -y 
sudo apt-get purge 'cuda-*' -y
sudo apt-get purge 'libcuda*' -y
sudo apt-get purge 'libcudnn*' -y
sudo apt-get autoremove -y
sudo apt-get autoclean -y
sudo apt-get update
```

## Remove the old repositories

```sh
sudo rm /etc/apt/sources.list.d/nvidia-diag-driver-local-384.66.list
sudo rm /etc/apt/sources.list.d/graphics-drivers-ubuntu-ppa-xenial.list
```

## Reboot and Check if all removed

```sh
sudo shutdown -r now
```

```sh
sudo dpkg --list | grep nvidia
sudo dpkg --list | grep cuda
sudo dpkg --list | grep libcudnn

lsmod | grep nvidia
```

## Revert `gcc` and `g++` to ver 5

```sh
sudo ln -s /usr/bin/gcc-5 /usr/bin/gcc -f
sudo ln -s /usr/bin/g++-5 /usr/bin/g++ -f
```

## Download `cuda`

```sh
cd ~/Downloads

wget https://developer.nvidia.com/compute/cuda/9.0/Prod/local_installers/cuda-repo-ubuntu1604-9-0-local_9.0.176-1_amd64-deb
mv cuda-repo-ubuntu1604-9-0-local_9.0.176-1_amd64-deb cuda-repo-ubuntu1604-9-0-local_9.0.176-1_amd64.deb
sudo dpkg -i cuda-repo-ubuntu1604-9-0-local_9.0.176-1_amd64.deb

wget https://developer.nvidia.com/compute/cuda/9.2/Prod/local_installers/cuda-repo-ubuntu1604-9-2-local_9.2.88-1_amd64.deb
sudo dpkg -i cuda-repo-ubuntu1604-9-2-local_9.2.88-1_amd64.deb

sudo apt-key add /var/cuda-repo-<version>/7fa2af80.pub
sudo apt-key adv --fetch-keys http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/7fa2af80.pub
sudo apt-get update
sudo apt-get install cuda-9-0 -y # cuda-9-2
```

## Env Update

```sh
sudo vim /etc/bash.bashrc
```
and replace the following:

```vim
### CUDA PATH
export CUDA_HOME="/usr/local/cuda-9.2"
export PATH="/usr/local/cuda-9.2/bin${PATH:+:${PATH}}"
export LD_LIBRARY_PATH="/usr/local/cuda-9.2/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}"
export LD_LIBRARY_PATH="/usr/local/cuda-9.2/include${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}"
```

## Reboot

```sh
sudo shutdown -r now
```

## Final check

```sh
lsmod | grep nvidia
```

