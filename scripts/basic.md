# Basics on Tensorflow


## Basic operation

pure ```python```:
```python
x = 1
y = x + 9
y
```


```tensorflow```:
```python
import tensorflow as tf

##### Construction #####
x = tf.constant(1)
y = tf.constant(9)

adder = tf.add(x, y)

##### Execution #####
sess = tf.Session()

result = sess.run(adder)
print(result)

sess.close()
```
or 
```python
import tensorflow as tf

##### Construction #####
x = tf.constant(1, name='x')
y = tf.Variable(x + 9, name='y')

model = tf.initialize_all_variables()

##### Execution #####
with tf.Session() as session:
    session.run(model)
    session.run(y)
```

## ```tensorflow``` Data Structure


All ```tensor``` have this objects.  

| OBJECT | DESCRIPTION | USAGE | EXAMPLE |
| :--- | :---------- | :------ | :------ |
| ```rank``` | Dimension | ```tensor.ndim``` | ```vector```: 1  ```matrix```: 2  ```ndarray``` or ```panel```: 3 |
| ```shape``` | Rows & Columns | ```tensor.shape``` | ```(4L,)``` |
| ```type``` | Data type | ```tensor.dtype``` | ```dtype('float64')``` |


All of the following ```methods``` can initiate ```tensor```.

* Constant Value Tensors  

>tf.zeros(shape, dtype=tf.float32, name=None)  
>tf.zeros_like(tensor, dtype=None, name=None, optimize=True)  
>tf.ones(shape, dtype=tf.float32, name=None)  
>tf.ones_like(tensor, dtype=None, name=None, optimize=True)  
>tf.fill(dims, value, name=None)  
>tf.constant(value, dtype=None, shape=None, name='Const', verify_shape=False)  

* Sequences  

>tf.linspace(start, stop, num, name=None)  
>tf.range(start, limit=None, delta=1, dtype=None, name='range')  

* Random Tensors  

>tf.random_normal(shape, mean=0.0, stddev=1.0, dtype=tf.float32, seed=None, name=None)  
>tf.truncated_normal(shape, mean=0.0, stddev=1.0, dtype=tf.float32, seed=None, name=None)  
>tf.random_uniform(shape, minval=0, maxval=None, dtype=tf.float32, seed=None, name=None)  
>tf.random_shuffle(value, seed=None, name=None)  
>tf.random_crop(value, size, seed=None, name=None)  
>tf.multinomial(logits, num_samples, seed=None, name=None)  
>tf.random_gamma(shape, alpha, beta=None, dtype=tf.float32, seed=None, name=None)  
>tf.set_random_seed(seed)  


* Variables  


>tf.Variable.__init__(initial_value=None, trainable=True, collections=None, validate_shape=True, caching_device=None, name=None, variable_def=None, dtype=None, expected_shape=None, import_scope=None)  
>tf.Variable(value, name=None, dtype=None)  
>tf.Variable.initialized_value()  
>tf.Variable.assign(value, use_locking=False)  



### Creation

* ```tf.constant()```  
* ```tf.convert_to_tensor()```  

#### Create 1D ```tensor```
```python
import tensorflow as tf
tmp = [1, 2.1, 5.44]
tf_tmp = tf.convert_to_tensor(tmp)
tf_tmp
--------------------------------------
<tf.Tensor 'Const:0' shape=(3,) dtype=float32>
--------------------------------------

with tf.Session() as ses:
    ses.run(tf_tmp).ndim
    ses.run(tf_tmp).shape
    ses.run(tf_tmp).dtype
    print(ses.run(tf_tmp))
    print(ses.run(tf_tmp)[0])
--------------------------------------
1
(3,)
dtype('float32')
[ 1.          2.0999999   5.44000006]
1.0
--------------------------------------
```

#### Create 2D ```tensor```
```python
import numpy as np
tmp = np.array([(1,1,1,1), list(range(0,4)), [13, 4 ,11, 6]])
tmp
#--------------------------------------#
array([[ 1,  1,  1,  1],
       [ 0,  1,  2,  3],
       [13,  4, 11,  6]])
#--------------------------------------#

tf_tmp = tf.convert_to_tensor(tmp)

with tf.Session() as ses:
    ses.run(tf_tmp).ndim
    ses.run(tf_tmp).shape
    ses.run(tf_tmp).dtype
    print(ses.run(tf_tmp))
    print(ses.run(tf_tmp)[1])
    print(ses.run(tf_tmp)[2, 2])
    print(ses.run(tf_tmp)[1:, (0, 2)])
#--------------------------------------#
2
(3, 4)
dtype('int64')
[[ 1  1  1  1]
 [ 0  1  2  3]
 [13  4 11  6]]
[0 1 2 3]
11
[[ 0  2]
 [13 11]]
#--------------------------------------#
```

#### Create 3D ```tensor```
```python
import numpy as np
tmp = np.arange(60).reshape(3,5,4)

tmp
#--------------------------------------#
array([[[ 0,  1,  2,  3],
        [ 4,  5,  6,  7],
        [ 8,  9, 10, 11],
        [12, 13, 14, 15],
        [16, 17, 18, 19]],

       [[20, 21, 22, 23],
        [24, 25, 26, 27],
        [28, 29, 30, 31],
        [32, 33, 34, 35],
        [36, 37, 38, 39]],

       [[40, 41, 42, 43],
        [44, 45, 46, 47],
        [48, 49, 50, 51],
        [52, 53, 54, 55],
        [56, 57, 58, 59]]])
#--------------------------------------#

tf_tmp = tf.convert_to_tensor(tmp)

with tf.Session() as ses:
    ses.run(tf_tmp).ndim
    ses.run(tf_tmp).shape
    ses.run(tf_tmp).dtype
    print(ses.run(tf_tmp)[1])
    print(ses.run(tf_tmp)[2, 2])
    print(ses.run(tf_tmp)[2, 2, 1])
    print(ses.run(tf_tmp)[1:, (0, 2), 3])
#--------------------------------------#
3
(3, 5, 4)
dtype('int64')
[[20 21 22 23]
 [24 25 26 27]
 [28 29 30 31]
 [32 33 34 35]
 [36 37 38 39]]
[48 49 50 51]
49
[[23 31]
 [43 51]]
#--------------------------------------#
```


### Construction
  

```python

```


### Execution

```python
tf.Session()

tf.Session().close()
```


