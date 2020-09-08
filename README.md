## cooja-docker
## Author: Namya Malik

A docker container that has all the dependencies to run the Contiki OS Cooja simulator. Instructions provided for machines with X11 support and machines without X11 support.

### Prerequisites
* Docker-desktop should be installed on your system. Make sure it is running.

### For machines with X11 support
* On a Linux host, the commands below should start the cooja GUI within a docker container. I borrowed this from another repo. I could have written my own Dockerfile but I am working on a Mac which does not have X11 support, so I would not have been able to test my Dockerfile on my machine. So I used another repo to provide instructions for machines with X11 and then figured out the functionality for machines without X11 (see next section)
```
docker run -it --rm -e DISPLAY --net=host sbungartz/cooja ant run
```
or (this command maps the display environment variable)
```
docker run -it --rm -e DISPLAY=$DISPLAY --net=host sbungartz/cooja ant run
```

* To see the full repo, see https://github.com/sbungartz/cooja-docker

### For machines without X11 support such as Macs
* Start VNC within docker container:
```
docker run -p 6080:80 -v /dev/shm:/dev/shm dorowu/ubuntu-desktop-lxde-vnc:trusty
```

* Once "RUNNING state" has begun from the previous command, open a browser and type the following:
```
localhost:6080
```

* This should open an X11 environment. Click "Connect", full-screen the window, click the "Start" application symbol at the bottom-left of the window, click "Accessories", click "LXTerminal" to open a terminal window

* Run the following `apt-get` commands:
```
apt-get update
```
```
apt-get -y install build-essential binutils-msp430 gcc-msp430 msp430-libc binutils-avr gcc-avr gdb-avr avr-libc avrdude binutils-arm-none-eabi gcc-arm-none-eabi gdb-arm-none-eabi openjdk-7-jdk openjdk-7-jre ant libncurses5-dev doxygen srecord git
```

* Clone the `contiki` repo:
```
git clone --recursive git://github.com/contiki-os/contiki.git contiki
```

* Export environment variables:
```
export JAVA_TOOL_OPTIONS="-Dfile.encoding=UTF8"
```
```
export JAVA_HOME="/usr/lib/jvm/java-7-openjdk-amd64"
```

* Navigate to cooja directory:
```
cd contiki/tools/cooja
```

* Compile and run cooja simulator to open GUI
```
ant run
```

### Background Info
X11 is needed for GUI interaction. 

### Helpful docker commands:
* Check running containers (and get info such as container id or name of container): `docker ps`

* Check all past containers: `docker ps -a`

* Copy from docker container to local: `docker cp containerId:docker/path/to/source local/path/to/destination`

* Stop a running container: `docker stop <containerId>`

* Remove a container: `docker rm <containerId>`

* Force remove all containers and free space: `docker system prune --force`

* Remove images and free space: `docker rmi imageID [imageID]`
