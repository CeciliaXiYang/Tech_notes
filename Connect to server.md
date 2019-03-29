## Method1  

- Install Anaconda  
   ```
   wget http://repo.continuum.io/archive/Anaconda3-4.0.0-Linux-x86_64.sh  
   bash Anaconda3-4.0.0-Linux-x86_64.sh
   ```

- Check which python in use  

   Anaconda has been installed in the server with pkgs. However, the default python version is in `/usr/bin/python` 
   Command `which python` could check which python we are using   

- Set the environment variable  
   ```
   vim ~/.bash_profile (or ~/.bashrc)
   Add export PATH="/opt/Anaconda2/bin:$PATH" in the end of .bashrc
   source ~/.bash_profile
   ```
   
- Check the added path: `echo $PATH`  
   
   `/opt/Anaconda2/bin` has been added into the front of the PATH  

   * folder in front of the PATH would be taken as the default version  

## Method2  

  `alias python='/opt/Anaconda2/bin/python2.7'`  

## Cause of error  
   - Lost of a '/' in front of the path -- '/opt/Anaconda2/bin'  
   - Wrongly spelled Anaconda2  

   Queston: Difference between `~/.bashrc` and `~/.bash_profile`  

## Anaconda on server: 
   reference: https://www.digitalocean.com/community/tutorials/how-to-install-anaconda-on-ubuntu-18-04-quickstart

## Jupyter notebook on server
   - Set up a SSL tunnel: `ssh me@remote.address -L127.0.0.1:3129:127.0.0.1:2018`  
   - Start server  
   - `$ jupyter notebook`  
   - Visit the server by: http://localhost:3129

