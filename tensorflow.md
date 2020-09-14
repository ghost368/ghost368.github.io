* installing correct nvidia drivers


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