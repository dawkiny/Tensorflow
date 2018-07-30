# Tips

## `is_training` Option Tensor


## Multiple `GPU`


```py
from tensorflow.python.client import device_lib
local_devices = device_lib.list_local_devices()
device_name_list = [d.name for d in local_devices]
print(device_name)

['/device:CPU:0', '/device:GPU:0', '/device:GPU:1']
```

