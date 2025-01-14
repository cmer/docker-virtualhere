# docker-virtualhere

> Info: This container was tested on and was developed for Linux hosts only! You might be able to convince other hosts to work as well but you are entering uncharted waters on your own risk ;) ...

[![automated](https://img.shields.io/docker/automated/cmer/virtualhere.svg)](https://hub.docker.com/r/cmer/virtualhere/)
[![build](https://img.shields.io/docker/build/cmer/virtualhere.svg)](https://hub.docker.com/r/cmer/virtualhere/)
[![pulls](https://img.shields.io/docker/pulls/cmer/virtualhere.svg)](https://hub.docker.com/r/cmer/virtualhere/)

[VirtualHere](https://www.virtualhere.com/) is a piece of software that allows you to share USB-devices (Scanner, Printer, Mouse, Keyboard etc.) over the network.

VirtualHere itself is not included in the docker-image directly but rather gets downloaded from the authors website upon the first start of the container. It should also auto-update on every restart.

For VirtualHere to work correctly you have to ensure that you run the container with access to your hosts USB-devices. This can for example be achieved by running in privileged mode (--privileged).

While the default port 7575 is exposed per default with this image, the usual Auto-Discovery based on Bonjour will not work unless you run the container on the host network. You can however enter the IP and port in the [Client](https://www.virtualhere.com/usb_client_software) manually if you choose not to do so.

Map the /data folder of this container to a folder on your host to get access to the config.ini file that allows you to enter your license information, change different parameters, choose which usb-devices to share etc.

To run on host network use:
~~~~
$ docker run -d -v /host/directory:/data --network=host --privileged --name cmer-virtualhere cmer/virtualhere:latest
~~~~
Otherwise use:
~~~~
$ docker run -d -v /host/directory:/data -p 7575:7575 --privileged --name cmer-virtualhere cmer/virtualhere:latest
~~~~
(Replace "/host/directory" with a valid directory on your host machine)

The trial-license allows you to share one usb-device. For multiple devices and more advanced features (such as traffic-encryption, user-authentication etc.), you will have to purchase a license from the author of VirtualHere. Always support a developers hard work if you think it is worth it!
