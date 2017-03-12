# Caffe


## Install `Caffe` from Source ( with pure Python )

```sh
sudo apt-get install --no-install-recommends build-essential cmake git gfortran libatlas-base-dev libboost-all-dev libgflags-dev libgoogle-glog-dev libhdf5-serial-dev libleveldb-dev liblmdb-dev libopencv-dev libprotobuf-dev libsnappy-dev protobuf-compiler python-all-dev python-dev python-h5py python-matplotlib python-numpy python-opencv python-pil python-pip python-protobuf python-scipy python-skimage python-sklearn
```

Download Source

```sh
# example location - can be customized
export CAFFE_ROOT=~/caffe
git clone https://github.com/NVIDIA/caffe.git $CAFFE_ROOT
```

```sh
sudo pip install -r $CAFFE_ROOT/python/requirements.txt
```

In case of error:

```sh
#cat $CAFFE_ROOT/python/requirements.txt | xargs -n1 sudo pip install
```
### Build with `cmake`

```sh
cd $CAFFE_ROOT
mkdir build
cd build
cmake ..
make --jobs=4

```

## Install `Caffe` from Source ( with Anaconda Python )

```sh
conda update conda

```

## Optional(install with separated environment) : 
```sh
conda create -n testcaffe python
source activate testcaffe
```

### Install `OpenCV`

```sh
conda install -c menpo opencv3
```

### Install defendencies

```sh
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install -y build-essential cmake git pkg-config
sudo apt-get install -y libprotobuf-dev libleveldb-dev libsnappy-dev protobuf-compiler
sudo apt-get install -y libatlas-base-dev 
sudo apt-get install -y --no-install-recommends libboost-all-dev
sudo apt-get install -y libgflags-dev libgoogle-glog-dev liblmdb-dev

```

### Build `Caffe`

Download `zip` [here](https://github.com/BVLC/caffe)


```sh
cd $CAFFE_HOME
mkdir build
cd build
cmake ..
make all
make install
make runtest
```

In case of error:

```sh
cd $CAFFE_HOME/python
conda install cython scikit-image ipython h5py nose pandas protobuf pyyaml jupyter
for req in $(cat requirements.txt); do pip install $req; done
cd ../build
make runtest
```

Add the module directory to your `$PYTHONPATH` by:
```sh
cd ../python
export PYTHONPATH=`pwd`${PYTHONPATH:+:${PYTHONPATH}}
```

### Test & Run

```sh
python -c "import caffe;print caffe.__version__"

```

```sh
jupyter notebook

```
