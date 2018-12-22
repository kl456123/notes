# How to adjust parameters


## leanrning rate
* exp lr decay
* const lr
use 1e-3 as initial lr for faster rcnn


## optimizer
use mometum sgd


## initializer
tf.truncate_normalization


## weights decay
```python
slim.l2_regularizer(weights_decay)
```

## clip gradients
`tf.clip_by_norm`
* note that it just normalizes a single gradients in tf


# some statistic
* recall(very important,make sure the performance,>0.8)
* fg/bg(make sure model is correct(e,g,fg/bg bigger than 30/512))
* recall_thresh(make sure capability of classification,>0.9*recall)

