Tool: MATLAB Engine for Python  
Python version: python2.7, 3.3, 3.4, 3.5  
Reference: https://www.youtube.com/watch?v=yhnB7zWgi_Q  

Steps:
1) `matlabroot` in MATLAB command window
   ans = "C:\Program Files\MATLAB\R2017b"
   
2) cmd as an administrator, run the following commands:  
   ```
   cd C:\Program Files\MATLAB\R2017b   
   cd extern\engines\python  
   python setup.py install  
   ```
   
3) Test if environment has been successfully configured with following code in python: 
   ```
   import matlab.engine
   eng = matlab.engine.start_matlab()
   tf = eng.isprime(37)
   print(tf)
   eng.eval("figure", nargout=0) # To show graphics figure
   ```
