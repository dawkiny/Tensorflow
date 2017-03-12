# Tensorflow


## Install `tensorflow`
```sh
conda create -n tensorflow python=3.5
source activate tensorflow
pip install --ignore-installed --upgrade \
 https://storage.googleapis.com/tensorflow/linux/gpu/tensorflow_gpu-1.0.0-cp35-cp35m-linux_x86_64.whl
 
```
CPU ONLY:
```sh
https://storage.googleapis.com/tensorflow/linux/cpu/tensorflow-1.0.0-cp35-cp35m-linux_x86_64.whl
```
GPU Support:
```sh
https://storage.googleapis.com/tensorflow/linux/gpu/tensorflow_gpu-1.0.0-cp35-cp35m-linux_x86_64.whl

```
In case of uninstallation:
```sh
conda env remove -n tensorflow
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

## Usage
* [Basics on Tensorflow](https://github.com/dawkiny/Tensorflow/blob/master/scripts/basic.md)
