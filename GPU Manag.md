## GPU monitoring  
  nvidia-smi  

## Show all processes using GPU  
  `ps -ef | grep python`  
  
  Refer to: https://askubuntu.com/questions/852206/what-does-ps-efgrep-processname-mean  
  ```
  ps: list processes
  -e: show all processes, not only processes belonging to current user
  -f: show the full name
  pass output of "ps -ef" as input of "grep python"
  grep: find out lines containing "python"
  ```

## Set Tensorflow to use partial of GPU   
  ```
  import tensorflow as tf
  config = tf.ConfigProto()
  config.gpu_options.per_process_gpu_memory_fraction = 0.1
  session = tf.Session(config=config)
  ```
  
  Refer to: https://www.tensorflow.org/tutorials/using_gpu  
  ** By default, tensorflow maps nearly all of the GPU memory of all GPUs visible to the process  
  
  Another option is to allocate as much GPU memory nased on runtime allocations, without releasing memory:   
  ```
  config = tf.ConfigProto()
  config.gpu_options.allow_growth = True
  session = tf.Session(config = config)
  ```
  
## Select a certain GPU to use:
  import os
  os.environ['CUDA_VISIBLE_DEVICES'] = '0' % Select the gpu_0 to use
  
  Refer to: https://www.cnblogs.com/darkknightzh/p/6591923.html
            http://www.acceleware.com/blog/cudavisibledevices-masking-gpus
  Q: When selecting the gpu, it would occupy the whole memory of that gpu to use?? How to solve this? 

## Check GPU or CPU in use:
  ```
  import tensorflow as tf
  sess = tf.Session(config=tf.ConfigProto(log_device_placement=True))  
  ```
  
## TensorFlow: InternalError: Blas SGEMM launch failed  
  ```
  if 'session' in locals() and session is not None:
    print('Close interactive session')
    session.close()
  ```
  
  Close interacitve sessions active on other processes (For jupyter notebook, restart the kernels)  
 
## If a TensorFlow operation has both CPU and GPU implementations, 
  the GPU devices will be given priority when the operation is assigned to a device.

## CUDA_OUT_OF_MEMORY warning  
  By default, tensorflow try to allocate a fraction per_process_gpu_memory_fraction of the GPU memory 
  to his process to avoid costly memory management. The default behavior takes ~95% of the memory. 
  
  Reference: https://stackoverflow.com/questions/39465503/cuda-error-out-of-memory-in-tensorflow
  
## Check theano use GPU or CPU:
  ```
  from theano import function, config, shared, tensor
  import numpy
  import time

  vlen = 10 * 30 * 768  # 10 x #cores x # threads per core
  iters = 1000

  rng = numpy.random.RandomState(22)
  x = shared(numpy.asarray(rng.rand(vlen), config.floatX))
  f = function([], tensor.exp(x).transfer(None))
  print(f.maker.fgraph.toposort())
  t0 = time.time()
  for i in range(iters):
      r = f()
  t1 = time.time()
  print("Looping %d times took %f seconds" % (iters, t1 - t0))
  print("Result is %s" % (numpy.asarray(r),))
  if numpy.any([isinstance(x.op, tensor.Elemwise) and
                ('Gpu' not in type(x.op).__name__)
                for x in f.maker.fgraph.toposort()]):
      print('Used the cpu')
  else:
      print('Used the gpu')
  ```
  
  Reference: http://deeplearning.net/software/theano/tutorial/using_gpu.html#testing-the-gpu
  
  
