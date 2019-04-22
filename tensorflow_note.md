### Ways of creating variables in tensorflow 
1. Placeholder() 
--> not trainable, i.e., cannot be reflected in `tf.trainable_variables()`

2. Variable() 
--> trainable, when new variable created with the same name, it will be distinguished with postfix. 
However, if variables with the same name are created under different name_scope, they can hold the same name. 

3. get_Variable() 
--> variable can be shared, distinguished by variable_scope

Reference: [https://blog.csdn.net/Jerr__y/article/details/70809528]
