# Basics on Tensorflow


## Basic operation

pure ```python```
```python
x = 1
y = x + 9
y
```


```tensorflow```
```python
import tensorflow as tf

x = tf.constant(1, name='x')
y = tf.Variable(x + 9, name='y')
y

model = tf.initialize_all_variables()

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

```python
import tensorflow as tf

# Create a variable.
w = tf.Variable(<initial-value>, name=<optional-name>)

# Use the variable in the graph like any Tensor.
y = tf.matmul(w, ...another variable or tensor...)

# The overloaded operators are available too.
z = tf.sigmoid(w + y)

# Assign a new value to the variable with `assign()` or a related method.
w.assign(w + 1.0)
w.assign_add(1.0)
```



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
--------------------------------------
array([[ 1,  1,  1,  1],
       [ 0,  1,  2,  3],
       [13,  4, 11,  6]])
--------------------------------------

tf_tmp = tf.convert_to_tensor(tmp)

with tf.Session() as ses:
    ses.run(tf_tmp).ndim
    ses.run(tf_tmp).shape
    ses.run(tf_tmp).dtype
    print(ses.run(tf_tmp))
    print(ses.run(tf_tmp)[1])
    print(ses.run(tf_tmp)[2, 2])
    print(ses.run(tf_tmp)[1:, (0, 2)])
--------------------------------------
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
--------------------------------------
```

#### Create 3D ```tensor```
```python
import numpy as np
tmp = np.arange(60).reshape(3,5,4)

tmp
--------------------------------------
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
--------------------------------------

tf_tmp = tf.convert_to_tensor(tmp)

with tf.Session() as ses:
    ses.run(tf_tmp).ndim
    ses.run(tf_tmp).shape
    ses.run(tf_tmp).dtype
    print(ses.run(tf_tmp)[1])
    print(ses.run(tf_tmp)[2, 2])
    print(ses.run(tf_tmp)[2, 2, 1])
    print(ses.run(tf_tmp)[1:, (0, 2), 3])
--------------------------------------
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
--------------------------------------
```

#### 

### Construction
```tf.placeholder()```
```python

images_placeholder = tf.placeholder(tf.float32, shape=(batch_size, IMAGE_PIXELS))
labels_placeholder = tf.placeholder(tf.int32, shape=(batch_size))
```

```python
inference() # 예측을 위해 네트워크가 진행하는데 필요한 만큼 그래프를 만듭니다.
loss()      # 추론(inference) 그래프에 손실(loss)을 발생시키는 데 필요한 연산을 추가합니다.
training()  # 손실 그래프에 그래디언트를 계산하고 적용하는 데 필요한 연산을 추가합니다.
```


### Execution

### 


```text
import tensorflow as tf

# 1x2 형렬을 만드는 Constant 연산을 생성합니다.
# 이 연산자는 기본 그래프의 노드로 추가됩니다.
#
# 생성자에 의해 반환된 값(matrix1)은 Constant 연산의 출력을 나타냅니다.
matrix1 = tf.constant([[3., 3.]])

# 2x1 행렬을 만드는 또 다른 Constant를 생성합니다.
matrix2 = tf.constant([[2.],[2.]])

# 'matrix1'과 'matrix2'를 입력으로 받는 Matmul 연산을 생성합니다.
# 반환값인 'product'는 행렬을 곱한 결과를 나타냅니다.
product = tf.matmul(matrix1, matrix2)


import tensorflow as tf
# 기본 그래프로 세션을 생성.
sess = tf.Session()

# matmul 연산을 실행하려면 matmul 연산의 출력을 나타내는 'product'를
# 인자로 넘겨주면서 세션의 'run()' 메소드를 호출합니다. 이렇게 호출하면
# matmul 연산의 출력을 다시 얻고 싶다는 뜻입니다.
#
# 연산이 필요로 하는 모든 입력은 세션에 의해 자동으로 실행됩니다.
# 일반적으로 병렬적으로 실행되지요.
#
# 따라서 'run(product)' 호출은 그래프 내의 세 개 연산을 실행하게 됩니다.
# 두 개의 상수와 matmul이 바로 그 연산이지요.
#
# 연산의 출력은 'result'에 numpy의 `ndarray` 객체 형태로 저장됩니다. 
result = sess.run(product)
print(result)
# ==> [[ 12.]]

# 다 끝났으면 세션을 닫아줍니다.
sess.close()
```
