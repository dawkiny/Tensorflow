# Tensorflow


## Install `tensorflow`
```sh
sudo apt-get install libcupti-dev

conda create -n Tensorflow python=3.5 ipykernel -y
source activate Tensorflow
python -m ipykernel install --user --name Tensorflow --display-name "Tensorflow Python3.5 (conda env)"

pip install --ignore-installed --upgrade \
 https://storage.googleapis.com/tensorflow/linux/gpu/tensorflow_gpu-1.0.0-cp35-cp35m-linux_x86_64.whl
 
```
GPU Support:
```sh
https://storage.googleapis.com/tensorflow/linux/gpu/tensorflow_gpu-1.0.0-cp35-cp35m-linux_x86_64.whl
```
CPU ONLY:
```sh
https://storage.googleapis.com/tensorflow/linux/cpu/tensorflow-1.0.0-cp35-cp35m-linux_x86_64.whl
```

In case of uninstallation:
```sh
conda env remove -n Tensorflow
```

### Test `tensorflow`

with `source activate tensorflow`:
```sh
python
```
```py
import tensorflow as tf
hello = tf.constant('Hello, TensorFlow!')
sess = tf.Session()
print(sess.run(hello))

```

In case of `ImportError` as the following:
```sh
ImportError: libcudart.so.8.0: cannot open shared object file: No such file or directory
```

```sh
sudo vi /etc/ld.so.conf.d/nvidia.conf
```

```vim
/usr/local/cuda-8.0/lib64
/usr/local/cuda-8.0/lib    # This line can be un-necessary : Check if it exists
```

Then
```sh
sudo ldconfig
```

## Usage
* [Basics on Tensorflow](https://github.com/dawkiny/Tensorflow/blob/master/scripts/basic.md)
