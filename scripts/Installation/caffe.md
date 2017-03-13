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

### Optional(install with separated environment) : 
```sh
conda create -n caffe python=3.5
source activate caffe
```

### Optional(Use python3.5) :

```sh
env PYTHON_CONFIGURE_OPTS="--enable-shared" pyenv install 3.5.1
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
mv Downloads/caffe-master.zip ~/apps
cd apps
unzip caffe-master.zip
mv caffe-master caffe
vi ~/.bashrc
```

```sh
cd caffe
cp Makefile.config.example Makefile.config
vi Makefile.config
```

```sh
# cuDNN acceleration switch (uncomment to build with cuDNN).
USE_CUDNN := 1

# Uncomment if you're using OpenCV 3
# OPENCV_VERSION := 3

# PYTHON_INCLUDE := /usr/include/python2.7 \
# 		/usr/lib/python2.7/dist-packages/numpy/core/include

# Anaconda Python distribution is quite popular. Include path:
# Verify anaconda location, sometimes it's in root.
ANACONDA_HOME := $(HOME)/apps/anaconda3
PYTHON_INCLUDE := $(ANACONDA_HOME)/include \
		$(ANACONDA_HOME)/include/python3.5 \
		$(ANACONDA_HOME)/lib/python3.5/site-packages/numpy/core/incl
    
# Uncomment to use Python 3 (default is Python 2)
PYTHON_LIBRARIES := boost_python3 python3.5m
# PYTHON_INCLUDE := /usr/include/python3.5m \
#                 /usr/lib/python3.5/dist-packages/numpy/core/include

# We need to be able to find libpythonX.X.so or .dylib.
# PYTHON_LIB := /usr/lib
PYTHON_LIB := $(ANACONDA_HOME)/lib

# Uncomment to support layers written in Python (will link against Python libs)
WITH_PYTHON_LAYER := 1

# Uncomment to use `pkg-config` to specify OpenCV library paths.
# (Usually not necessary -- OpenCV libraries are normally installed in one of the above $LIBRARY_DIRS.)
# USE_PKG_CONFIG := 1

```

```sh
# CAFFE PATH
export CAFFE_HOME="/home/pydemia/apps/caffe"
```

```sh

cd $CAFFE_HOME
mkdir build
cd build
cmake ..
make all
make install
make runtest
```


```sh

cd $CAFFE_HOME
mkdir build
cd build
cmake .. -DPYTHON_INCLUDE_DIR=~/.pyenv/versions/3.5.1/include/python3.5m -DPYTHON_INCLUDE_DIR2=~/.pyenv/versions/3.5.1/include/python3.5m -DPYTHON_LIBRARY=~/.pyenv/versions/3.5.1/lib/libpython3.so -Dpython_version=3 ../caffe
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
python -c "import caffe;print(caffe.__version__)"

```

```sh
jupyter notebook

```
