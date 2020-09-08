# cooja-docker

A docker container that has all the dependencies to run the Contiki OS Cooja simulator. 

## INSTALLATION

### Prerequisites
* Docker-desktop should be installed on your system. Make sure it is running.

### For machines with X11 support
* On a Linux host, this command should start the cooja GUI within a docker container (borrowed from another repo):
```
docker run -it --rm -e DISPLAY --net=host sbungartz/cooja ant run
```
or 
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

### Miscellaneous
X11 is needed for GUI interaction. 

### Helpful docker commands:
* Check running containers (and get info such as container id or name of container): `docker ps`

* Check all past containers: `docker ps -a`

* Copy from docker container to local: `docker cp containerId:docker/path/to/source local/path/to/destination`

* Stop a running container: `docker stop <containerId>`

* Remove a container: `docker rm <containerId>`

* Force remove all containers and free space: `docker system prune --force`

* Remove images and free space: `docker rmi imageID [imageID]`

## ASSIGNMENTS
* For a tutorial/sample application of Cooja, see https://d18ky98rnyall9.cloudfront.net/P45NLC5yEeiHlgpAux3xng_3ff0df602e7211e8a7c4656e953f60b9_CoojaManual.pdf?Expires=1594684800&Signature=N0DMMRLANEQ6HfKu0arwoSGFGbr5F39ZI3u2hfVXQy5KN9OwK-l3Ndn1tJVo2MZSlh83naaAJ65k54W2f0fVLuB3u7vqva7qZjvpsVC5JO2XyPPwzC3uWFxnR2ObNTTjXNMkhrNjLJeopW0wuC5vsIys4u982RcefuxF66NrfEw_&Key-Pair-Id=APKAJLTNE6QMUY6HBC5A
* For the first Coursera assignment, see https://d18ky98rnyall9.cloudfront.net/Shw_8nLBEeiMOxLWp7wpfg_4a5be0b072c111e89508a947a324f3d8_Cooja_task.pdf?Expires=1594684800&Signature=E1q3i9s6QveUCdYZ3UEUheFJJ7nG3qiPUjptVyMcjpTaoiyuuTnAojRmPiYFE1CSn3Db6DSxcEuVMql50Kl4ZXLANulFCUvFwC~WB1hFnvD~L9BeY5500lSacw4nDNtjhp3lwifgrZzxQVDwpt8AYe8w~br4VgIQsP36OHaBGvM_&Key-Pair-Id=APKAJLTNE6QMUY6HBC5A
* For the second Coursera assignment, see https://d18ky98rnyall9.cloudfront.net/_3cfb6de0feadf7d84b6072ca68279dc9_Peer-assignment-2---Energy-estimation.pdf?Expires=1594684800&Signature=OdTkmTP5rlamb5ibQ9uC0zGQJbkYttGRFrkdd0GCdboRfp9-7l7gZUdXGkNhMpeMZpMC29u4nhqrBBl8QHe5ttF9INOIJTcHC6X4GoUw69JKaT1St9DLE30QN5kLcsppWB1~M6Ih4jFIKPqieSCpA1HPzH96VBgmRj5ryQ3qM~w_&Key-Pair-Id=APKAJLTNE6QMUY6HBC5A
