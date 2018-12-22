# some notes about tensorflow


* gpu data cannot be accessed from cpu device directly
* tensorflow automatic select device


* default format is 'nhwc'
* slim.fully_connected is different with that of caffe
* tf.variable_scope and tf.name_scope
* pad style of tensorflow is different with that of caffe
* initialization of variable or assign
* get tensor
```
graph = tf.get_default_graph()
graph.get_tensor_by_name()
tf.get_collections()
```
* slim.add_arg_scope
* nametuple
