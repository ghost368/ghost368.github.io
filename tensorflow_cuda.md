* installing correct nvidia drivers (by default usually the open-source nouveau driver is installed)
* on Ubuntu can do this by running 
```
ubuntu-drivers devices
```
and if nvidia driver is recommended, can simply run
```
sudo ubuntu-drivers autoinstall
```
(on fedora it's more complicated, check online)

* CUDA and CuDNN using conda vs manual
	- the easiest way to install CUDA/CuDNN is to simply create a conda env and install tensorflow-gpu there via conda,
	this will install CUDA inside the env
	- conda is by far the easiest way of installation but we are forced to use conda for env management (can try to install packages
	via poetry on top but there may be some conflicts)
	- for prototyping and research **definitely** choose conda and can even manage env using conda env file
	- if it's in prod, can decide to use manual installation (maybe even inside docker container) and pure pip packages
	- **below is the way to manually install CUDA/CuDNN (in Ubuntu)**
	



* installing CUDA
	- down the needed version .deb file form CUDA website https://developer.nvidia.com/cuda-10.0-download-archive?target_os=Linux&target_arch=x86_64&target_distro=Ubuntu&target_version=1804&target_type=debnetwork

	- load the .deb file (using gui or wget) and run
	```
	sudo dpkg -i cuda-repo-ubuntu1804_10.1.168-1_amd64.deb
	sudo apt-key adv --fetch-keys https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/7fa2af80.pub
	sudo apt-get install cuda-10-1=10.1.168-1
	```

* installing CuDNN
	- go to https://developer.nvidia.com/cudnn, install the needed .deb file manually (requires sign up etc)
	- load 3 .deb files where needed (Runtime, Developer and Code Samples, more details here https://medium.com/analytics-vidhya/how-to-set-up-tensorflow-gpu-on-ubuntu-18-04-lts-7a09ffd5f30f#564e)
	for the installed CUDA version
	- 

###installing tensorflow:

* pip vs conda
	- can install using pip (incl. poetry that is pip-based) conda
	- I work with poetry, so prefer to use pip
	- for this need to manually install CUDA and CuDNN globally on the linux OS, 
	then can install compatible tensorflow versions inside environments
	- if using conda : can install tensorflow-gpu, cudatoolkit and cudnn packages from conda 
	channels (this requires only nvidia driver in the linux OS)
	- with conda can installed different versions of cuda, cudnn tensorflow in different envs


* to correctly install tensorflow with gpu support need a correct version combination of nvidia driver, 
cuda, CuDNN and tensorflow

* appropriate nvidia driver is needed to run gpu-accelerated tensorflow, check recommendation using 
```ubuntu-drivers devices``` (though slightly different versions to the recommended one may work well too)

* to check the current driver : run ```nvidia-smi```

* to install nvidia driver run ```sudo apt-get install nvidia-440``` (e.g. for 440 version), e.g. necessary 
if nvidia-smi commands does not show anything or you want to change the driver version


* compatibility tables for versions may be found online 

* before install cuda, cudnn may be worth removing already installed old versions with all deps: use
```
sudo apt-get purge "cuda*"
sudo apt-get purge "*cublas*"
sudo apt-get autoremove
sudo apt-get clean
```
(autoremove with remove all unused leftovers, purge differs from remove in that it removes dependencies)



* also the official tensorflow site (https://www.tensorflow.org/install/gpu) has up-to-date instruction, e.g. here the one for Ubuntu 18.04
(cd to folder where you are ok to download the .deb files)
```
# Add NVIDIA package repositories
wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/cuda-repo-ubuntu1804_10.1.243-1_amd64.deb
sudo apt-key adv --fetch-keys https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/7fa2af80.pub
sudo dpkg -i cuda-repo-ubuntu1804_10.1.243-1_amd64.deb
sudo apt-get update
wget http://developer.download.nvidia.com/compute/machine-learning/repos/ubuntu1804/x86_64/nvidia-machine-learning-repo-ubuntu1804_1.0.0-1_amd64.deb
sudo apt install ./nvidia-machine-learning-repo-ubuntu1804_1.0.0-1_amd64.deb
sudo apt-get update

# Install NVIDIA driver
sudo apt-get install --no-install-recommends nvidia-driver-450
# Reboot. Check that GPUs are visible using the command: nvidia-smi

# Install development and runtime libraries (~4GB)
sudo apt-get install --no-install-recommends \
    cuda-10-1 \
    libcudnn7=7.6.5.32-1+cuda10.1  \
    libcudnn7-dev=7.6.5.32-1+cuda10.1


# Install TensorRT. Requires that libcudnn7 is installed above.
sudo apt-get install -y --no-install-recommends libnvinfer6=6.0.1-1+cuda10.1 \
    libnvinfer-dev=6.0.1-1+cuda10.1 \
    libnvinfer-plugin6=6.0.1-1+cuda10.1
```

* after that tensorflow-gpu can be installed using poetry or pip (version 2.2.0 works well with the cuda, cudnn versions above)

* it may be needed to update environmental variables (append export lines to ~/.bashrc):

	- had to add this 
	```
	export LD_LIBRARY_PATH=/usr/local/cuda-10.2/lib64
	export PATH=/usr/local/cuda/bin:$PATH
	```
	- cuda installation above will create several packages in /usr/local (like cuda, cuda-10.1, cuda-10.2), 
	and the necessary libs may be in lib64 subfolders in any of them;
	e.g. for the lib that LD_LIBRARY_PATH is responsible for this was cuda-10.2
	- run in ipython 
	```
	import tensorflow as tf
	tf.test.is_gpu_available()
	```
	(if error and some libs are not found - look for them in the lib64 packages, adjust PATH and LD_LIBRARY_PATH if 
	necessary)
