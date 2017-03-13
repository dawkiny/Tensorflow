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
```y


### Install `OpenCV`

```sh
conda install -c menpo opencv3
```

### Install defendencies

```sh
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install -y build-essential cmake git pkg-config
sudo apt-get install -y libprotobuf-dev libleveldb-dev libsnappy-dev libopencv-dev libhdf5-serial-dev protobuf-compiler libatlas-base-dev libgflags-dev libgoogle-glog-dev liblmdb-dev
sudo apt-get install libboost-all-dev
sudo apt-get install --no-install-recommends libboost-all-dev
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
# HOME := /home/pydemia
ANACONDA_HOME := $(HOME)/apps/anaconda3
PYTHON_LIBRARIES := $(ANACONDA_HOME)/lib \
		$(ANACONDA_HOME)/lib/python3.5/site-packages
INCLUDE_DIRS := $(ANACONDA_HOME)/include \
		$(ANACONDA_HOME)/include/python3.5m \
		$(ANACONDA_HOME)/lib/python3.5/site-packages/numpy/core/include

# Uncomment to use Python 3 (default is Python 2)
# PYTHON_LIBRARIES += boost_python3 python3.5m
# PYTHON_INCLUDE := /usr/include/python3.5m \
#                 /usr/lib/python3.5/dist-packages/numpy/core/include

# We need to be able to find libpythonX.X.so or .dylib.
# PYTHON_LIB := /usr/lib
PYTHON_LIB := $(ANACONDA_HOME)/lib

# Homebrew installs numpy in a non standard path (keg only)
PYTHON_INCLUDE += $(dir $(shell python -c 'import numpy.core; print(numpy.core.__file__)'))/include
PYTHON_LIB += $(shell brew --prefix numpy)/lib

# Uncomment to support layers written in Python (will link against Python libs)
WITH_PYTHON_LAYER := 1

# Whatever else you find you need goes here.
INCLUDE_DIRS := $(PYTHON_INCLUDE) #/usr/local/include
LIBRARY_DIRS := $(PYTHON_LIB) #/usr/local/lib /usr/lib

# If Homebrew is installed at a non standard location (for example your home directory) and you use it for general dependencies
INCLUDE_DIRS += $(shell brew --prefix)/include
LIBRARY_DIRS += $(shell brew --prefix)/lib

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
cmake .. -DPYTHON_EXECUTABLE=/home/pydemia/apps/anaconda3/bin/python3.5 -DPYTHON_INCLUDE_DIR=/home/pydemia/apps/anaconda3/include/python3.5m -DPYTHON_LIBRARY=/home/pydemia/apps/anaconda3/lib/libpython3.so -DBOOST_INCLUDEDIR=

../caffe
make all
make install
make runtest
```

Messeges:
```sh

-- The C compiler identification is GNU 5.4.0
-- The CXX compiler identification is GNU 5.4.0
-- Check for working C compiler: /usr/bin/cc
-- Check for working C compiler: /usr/bin/cc -- works
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Detecting C compile features
-- Detecting C compile features - done
-- Check for working CXX compiler: /usr/bin/c++
-- Check for working CXX compiler: /usr/bin/c++ -- works
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Looking for pthread.h
-- Looking for pthread.h - found
-- Looking for pthread_create
-- Looking for pthread_create - not found
-- Looking for pthread_create in pthreads
-- Looking for pthread_create in pthreads - not found
-- Looking for pthread_create in pthread
-- Looking for pthread_create in pthread - found
-- Found Threads: TRUE  
-- Boost version: 1.58.0
-- Found the following Boost libraries:
--   system
--   thread
--   filesystem
--   chrono
--   date_time
--   atomic
-- Found GFlags: /usr/include  
-- Found gflags  (include: /usr/include, library: /usr/lib/x86_64-linux-gnu/libgflags.so)
-- Found Glog: /usr/include  
-- Found glog    (include: /usr/include, library: /usr/lib/x86_64-linux-gnu/libglog.so)
-- Found Protobuf: /usr/lib/x86_64-linux-gnu/libprotobuf.so  
-- Found PROTOBUF Compiler: /usr/bin/protoc
-- Found HDF5: /home/pydemia/apps/anaconda3/lib/libhdf5_hl.so;/home/pydemia/apps/anaconda3/lib/libhdf5.so;/home/pydemia/apps/anaconda3/lib/libhdf5_hl.so;/home/pydemia/apps/anaconda3/lib/libhdf5.so;/usr/lib/x86_64-linux-gnu/librt.so;/usr/lib/x86_64-linux-gnu/libpthread.so;/home/pydemia/apps/anaconda3/lib/libz.so;/usr/lib/x86_64-linux-gnu/libdl.so;/usr/lib/x86_64-linux-gnu/libm.so (found version "1.8.17") 
-- Found LMDB: /usr/include  
-- Found lmdb    (include: /usr/include, library: /usr/lib/x86_64-linux-gnu/liblmdb.so)
-- Found LevelDB: /usr/include  
-- Found LevelDB (include: /usr/include, library: /usr/lib/x86_64-linux-gnu/libleveldb.so)
-- Found Snappy: /usr/include  
-- Found Snappy  (include: /usr/include, library: /usr/lib/x86_64-linux-gnu/libsnappy.so)
-- CUDA detected: 8.0
-- Found cuDNN: ver. 5.1.10 found (include: /usr/local/cuda-8.0/include, library: /usr/local/cuda-8.0/lib64/libcudnn.so)
-- Added CUDA NVCC flags for: sm_61
-- OpenCV found (/home/pydemia/apps/anaconda3/share/OpenCV)
-- Found Atlas: /usr/include  
-- Found Atlas (include: /usr/include, library: /usr/lib/libatlas.so)
-- Found PythonInterp: /home/pydemia/apps/anaconda3/bin/python3.5 (found suitable version "3.5.3", minimum required is "2.7") 
-- Found PythonLibs: /home/pydemia/apps/anaconda3/lib/libpython3.so (found suitable version "3.5.3", minimum required is "2.7") 
-- Found NumPy: /home/pydemia/apps/anaconda3/lib/python3.5/site-packages/numpy/core/include (found suitable version "1.11.3", minimum required is "1.7.1") 
-- NumPy ver. 1.11.3 found (include: /home/pydemia/apps/anaconda3/lib/python3.5/site-packages/numpy/core/include)
-- Boost version: 1.58.0
-- Found the following Boost libraries:
--   python
-- Could NOT find Doxygen (missing:  DOXYGEN_EXECUTABLE) 
-- Found Git: /usr/bin/git (found version "2.7.4") 
-- 
-- ******************* Caffe Configuration Summary *******************
-- General:
--   Version           :   1.0.0-rc5
--   Git               :   unknown
--   System            :   Linux
--   C++ compiler      :   /usr/bin/c++
--   Release CXX flags :   -O3 -DNDEBUG -fPIC -Wall -Wno-sign-compare -Wno-uninitialized
--   Debug CXX flags   :   -g -fPIC -Wall -Wno-sign-compare -Wno-uninitialized
--   Build type        :   Release
-- 
--   BUILD_SHARED_LIBS :   ON
--   BUILD_python      :   ON
--   BUILD_matlab      :   OFF
--   BUILD_docs        :   ON
--   CPU_ONLY          :   OFF
--   USE_OPENCV        :   ON
--   USE_LEVELDB       :   ON
--   USE_LMDB          :   ON
--   USE_NCCL          :   OFF
--   ALLOW_LMDB_NOLOCK :   OFF
-- 
-- Dependencies:
--   BLAS              :   Yes (Atlas)
--   Boost             :   Yes (ver. 1.58)
--   glog              :   Yes
--   gflags            :   Yes
--   protobuf          :   Yes (ver. 2.6.1)
--   lmdb              :   Yes (ver. 0.9.17)
--   LevelDB           :   Yes (ver. 1.18)
--   Snappy            :   Yes (ver. 1.1.3)
--   OpenCV            :   Yes (ver. 3.2.0)
--   CUDA              :   Yes (ver. 8.0)
-- 
-- NVIDIA CUDA:
--   Target GPU(s)     :   Auto
--   GPU arch(s)       :   sm_61
--   cuDNN             :   Yes (ver. 5.1.10)
-- 
-- Python:
--   Interpreter       :   /home/pydemia/apps/anaconda3/bin/python3.5 (ver. 3.5.3)
--   Libraries         :   /home/pydemia/apps/anaconda3/lib/libpython3.so (ver 3.5.3)
--   NumPy             :   /home/pydemia/apps/anaconda3/lib/python3.5/site-packages/numpy/core/include (ver 1.11.3)
-- 
-- Documentaion:
--   Doxygen           :   No
--   config_file       :   
-- 
-- Install:
--   Install path      :   /home/pydemia/apps/caffe-master/build/install
-- 
-- Configuring done
CMake Warning (dev) in src/caffe/CMakeLists.txt:
  Policy CMP0022 is not set: INTERFACE_LINK_LIBRARIES defines the link
  interface.  Run "cmake --help-policy CMP0022" for policy details.  Use the
  cmake_policy command to set the policy and suppress this warning.

  Target "caffe" has an INTERFACE_LINK_LIBRARIES property which differs from
  its LINK_INTERFACE_LIBRARIES properties.

  INTERFACE_LINK_LIBRARIES:

    proto;/usr/lib/x86_64-linux-gnu/libboost_system.so;/usr/lib/x86_64-linux-gnu/libboost_thread.so;/usr/lib/x86_64-linux-gnu/libboost_filesystem.so;/usr/lib/x86_64-linux-gnu/libboost_chrono.so;/usr/lib/x86_64-linux-gnu/libboost_date_time.so;/usr/lib/x86_64-linux-gnu/libboost_atomic.so;/usr/lib/x86_64-linux-gnu/libpthread.so;/usr/lib/x86_64-linux-gnu/libglog.so;/usr/lib/x86_64-linux-gnu/libgflags.so;$<$<NOT:$<CONFIG:DEBUG>>:/usr/lib/x86_64-linux-gnu/libprotobuf.so>;$<$<CONFIG:DEBUG>:/usr/lib/x86_64-linux-gnu/libprotobuf.so>;-lpthread;/home/pydemia/apps/anaconda3/lib/libhdf5_hl.so;/home/pydemia/apps/anaconda3/lib/libhdf5.so;/home/pydemia/apps/anaconda3/lib/libhdf5_hl.so;/home/pydemia/apps/anaconda3/lib/libhdf5.so;/usr/lib/x86_64-linux-gnu/librt.so;/usr/lib/x86_64-linux-gnu/libpthread.so;/home/pydemia/apps/anaconda3/lib/libz.so;/usr/lib/x86_64-linux-gnu/libdl.so;/usr/lib/x86_64-linux-gnu/libm.so;/home/pydemia/apps/anaconda3/lib/libhdf5_hl.so;/home/pydemia/apps/anaconda3/lib/libhdf5.so;/home/pydemia/apps/anaconda3/lib/libhdf5_hl.so;/home/pydemia/apps/anaconda3/lib/libhdf5.so;/usr/lib/x86_64-linux-gnu/librt.so;/usr/lib/x86_64-linux-gnu/libpthread.so;/home/pydemia/apps/anaconda3/lib/libz.so;/usr/lib/x86_64-linux-gnu/libdl.so;/usr/lib/x86_64-linux-gnu/libm.so;/usr/lib/x86_64-linux-gnu/liblmdb.so;/usr/lib/x86_64-linux-gnu/libleveldb.so;/usr/local/cuda-8.0/lib64/libcudart.so;/usr/local/cuda-8.0/lib64/libcurand.so;/usr/local/cuda-8.0/lib64/libcublas.so;/usr/local/cuda-8.0/lib64/libcudnn.so;opencv_core;opencv_highgui;opencv_imgproc;opencv_imgcodecs;/usr/lib/liblapack.so;/usr/lib/libcblas.so;/usr/lib/libatlas.so;/usr/lib/x86_64-linux-gnu/libboost_python.so

  LINK_INTERFACE_LIBRARIES:

    proto;/usr/lib/x86_64-linux-gnu/libboost_system.so;/usr/lib/x86_64-linux-gnu/libboost_thread.so;/usr/lib/x86_64-linux-gnu/libboost_filesystem.so;/usr/lib/x86_64-linux-gnu/libboost_chrono.so;/usr/lib/x86_64-linux-gnu/libboost_date_time.so;/usr/lib/x86_64-linux-gnu/libboost_atomic.so;/usr/lib/x86_64-linux-gnu/libpthread.so;/usr/lib/x86_64-linux-gnu/libglog.so;/usr/lib/x86_64-linux-gnu/libgflags.so;/usr/lib/x86_64-linux-gnu/libprotobuf.so;-lpthread;/home/pydemia/apps/anaconda3/lib/libhdf5_hl.so;/home/pydemia/apps/anaconda3/lib/libhdf5.so;/home/pydemia/apps/anaconda3/lib/libhdf5_hl.so;/home/pydemia/apps/anaconda3/lib/libhdf5.so;/usr/lib/x86_64-linux-gnu/librt.so;/usr/lib/x86_64-linux-gnu/libpthread.so;/home/pydemia/apps/anaconda3/lib/libz.so;/usr/lib/x86_64-linux-gnu/libdl.so;/usr/lib/x86_64-linux-gnu/libm.so;/home/pydemia/apps/anaconda3/lib/libhdf5_hl.so;/home/pydemia/apps/anaconda3/lib/libhdf5.so;/home/pydemia/apps/anaconda3/lib/libhdf5_hl.so;/home/pydemia/apps/anaconda3/lib/libhdf5.so;/usr/lib/x86_64-linux-gnu/librt.so;/usr/lib/x86_64-linux-gnu/libpthread.so;/home/pydemia/apps/anaconda3/lib/libz.so;/usr/lib/x86_64-linux-gnu/libdl.so;/usr/lib/x86_64-linux-gnu/libm.so;/usr/lib/x86_64-linux-gnu/liblmdb.so;/usr/lib/x86_64-linux-gnu/libleveldb.so;/usr/local/cuda-8.0/lib64/libcudart.so;/usr/local/cuda-8.0/lib64/libcurand.so;/usr/local/cuda-8.0/lib64/libcublas.so;/usr/local/cuda-8.0/lib64/libcudnn.so;opencv_core;opencv_highgui;opencv_imgproc;opencv_imgcodecs;/usr/lib/liblapack.so;/usr/lib/libcblas.so;/usr/lib/libatlas.so;/usr/lib/x86_64-linux-gnu/libboost_python.so

This warning is for project developers.  Use -Wno-dev to suppress it.

-- Generating done
-- Build files have been written to: /home/pydemia/apps/caffe-master/build

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
