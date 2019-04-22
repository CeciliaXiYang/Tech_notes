### Ways of creating variables in tensorflow 
1. Placeholder() 
--> not trainable, i.e., cannot be reflected in `tf.trainable_variables()`

2. Variable() 
--> trainable, when new variable created with the same name, it will be distinguished with postfix. 
However, if variables with the same name are created under different name_scope, they can hold the same name. 

3. get_Variable() 
--> variable can be shared, distinguished by variable_scope

Reference: [https://blog.csdn.net/Jerr__y/article/details/70809528]

```
import tensorflow as tf

config = tf.ConfigProto()
config.gpu_options.allow_growth = True
sess = tf.Session(config=config)

with tf.name_scope('nsc1'):
    v1 = tf.Variable([1], name='v1')
    with tf.variable_scope('vsc1'):
        v2 = tf.Variable([1], name='v2')
#         v3 = tf.get_variable(name='v3', shape=[])
#     with tf.variable_scope('vsc2'):
#         v4 = tf.get_variable(name='v3', shape=[])
print ('v1.name: ', v1.name)
print ('v2.name: ', v2.name)
# print ('v3.name: ', v3.name)
# print ('v4.name: ', v4.name)

with tf.name_scope('nsc2'):
    with tf.variable_scope('vsc2'):
        v4 = tf.Variable([1], name='v2')
print ('v4.name: ', v4.name)
```
