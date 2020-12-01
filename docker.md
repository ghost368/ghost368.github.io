
* install docker
```sudo apt-get update```
remove old versions
sudo systemctl enable docker	```
sudo apt-get remove docker docker-engine docker.io
```
run 
```
sudo apt install docker.io
```
can use 
```
sudo systemctl start docker
sudo systemctl enable docker
sudo systemctl status docker
```


* setup using docker for non-root user
```
sudo groupadd docker
sudo usermod -aG docker $USER
```
then in each process log in via running
```
newgrp docker
```
and can use docker w/o sudo in the current process



* commands
	* ```docker run```

	* ```docker run -it contname sh``` : running interactive shell inside container

	* ```docker pull``` :  fetches image from Docker registry
	* ```docker ps ``` : list of current running containers, with -a it shows all containers run before

	* ```docker ps -a -q``` : get stopped containers ids
	* ```docker rm IDs``` : rm containers (need ids; or can use ```docker container prune```)

	* ```docker images``` : list downloaded images
	images can have parents j- other images on which they are based


* creating images using Docker file

	- commands in the Dockerfile are very similar to linux commands

	- example of a Docker file
	```
		# specifying base image
	  1 FROM python:3
	  2
	  3 # set a directory for the app
	  4 WORKDIR /usr/src/app
	  5
	  6 # copy all the files from the current local app directory (git repo on local OS) to the container
	  7 COPY . .
	  8
	  9 # install dependencies (for poetry this can be poetry install command)
	 10 RUN pip install --no-cache-dir -r requirements.txt
	 11
	 12 # tell the port number the container should expose
	 13 EXPOSE 5000
	 14
	 15 # run the command for running the application (for a flask application -- this is simply calling the main .py file)
	 16 CMD ["python", "./app.py"]
	```

* build docker image using Dockerfile in the app folder
```
docker build /path/to/Dockerfile/rootdir -t image_name
```