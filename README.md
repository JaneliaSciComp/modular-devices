#modular-devices

Authors:

    Peter Polidoro <polidorop@janelia.hhmi.org>

License:

    BSD

##Introduction

Modular devices are combinations of open source object oriented
hardware, firmware, and software.

Modular devices extend object oriented software concepts into object
oriented hardware, allowing you to create hardware objects with
methods for executing actions, parameters for passing information to
the methods, fields for storing data, and callbacks for executing
actions from internal and external triggers and interrupts.

Modular devices have methods that can be executed locally or remotely
over a communication bus or channel with a client/server architecture.

Object oriented hardware is a mixture of processors, electronics, and
mechanics for interacting with, sensing, and controlling things in the
physical world. Each hardware object can be used independently or
combined like software objects to create more complex systems. The
hardware objects can be implemented in a variety of form factors. Some
form factors might be designed to be as small an inexpensive as
possible, while others might be larger with more features or capacity,
but every object has its own processor, with one or more communication
channels, and can be used on its own or combined with any other
hardware object, regardless of form factor. Hardware objects can scale
both up, by combining many of them together when large complicated
systems are needed, and scale down, so only a single hardware object
is necessary when needs are small and simple, minimizing cost and
component count.

Object oriented firmware/software server objects run on the hardware
objects and provide the interface necessary to interact with and
control the device. Each firmware/software server object adds a set of
methods, parameters, fields, and callbacks to the device. Every device
may consist of several layers of firmware/software server
objects. Each layer extends or modifies the layer beneath it, like
inheritance and composition in traditional object oriented
software. Lower layers may provide general features specific to the
particular hardware it is running on, while higher layers may add
features specific to the particular task the user may want to run or
hardware connected to the device. Firmware/software server objects are
written to maximize code reuse and separation of concerns.

Object oriented firmware/software client objects may be run on other
modular devices or on host computers connected to one or more modular
devices. The client software may be written in almost any language
capable of writing strings over the communication channel to the
modular device. Only one small client software driver should be
necessary in each language to talk to all firmware and hardware
objects. When the client software object initializes, it asks the
modular devices about its methods, parameters, fields, and callbacks,
and then uses that information to create the client object. So new or
modified modular devices can be connected to a client object and
controlled without the user needing to change or update the client
object code. Once the client has connected to the server, other
software may interact with the client, calling methods on the local
client object that automatically call the remote methods on the
modular device over the communication channel.

##Details

Modular devices are computers or electronics with microprocessors that
implement
the
[modular device protocol](https://github.com/janelia-modular-devices/modular_device_protocol.git) in
software or firmware.

Modular device servers consist of one or more methods that perform
some action. Each method takes zero or more parameters to specify the
action and methods may or may not return a value. Parameters and
return values can be any JSON type, including objects with key/value
pairs, arrays with an ordered collection of values, strings, numbers,
booleans, or null. Fields are used for storing data in the
device. Callbacks are used to execute actions from internal and
external triggers and interrupts.

Server methods may be triggered by changes on the local device, such
as timers expiring, buttons pressed, encoders turned, or through a GUI
or command line. Alternatively, server methods may be triggered by
external sources such as TTL signals or calls from modular device
clients through communication channels.

Modular device clients call server methods by sending the server
requests and the server handles the request and sends back a response
to the client.

Modular devices can be both clients and/or servers and devices
communicate with one another using [JSON](http://www.json.org/)
strings. Any communication channel capable of sending and receiving
JSON strings can used to connect modular devices to each
other. Servers may listen for client method calls on multiple
communication channels simultaneously and a device may use a single
communication channel for both server and client communications.

Modular devices implemented on Arduino-like boards and processors
communicate over serial UART channels. Arduino-like modular devices
can connect to each other's UART channels and call each other's
methods. Host computers such as desktops, laptops, and Raspberry
Pi-like single board computers can be used as clients to communicate
to Arduino-like modular device servers over a USB serial
port. Computers may be servers as well as clients and modular devices
may consist of more than one server and/or client.

Any programming language capable of processing JSON strings and
sending and receiving them over a serial port can be used as a client
to call methods on modular device servers. Users can interact with
remote modular devices over a serial port using simple serial
terminals, such as the Arduino IDE serial monitor, cutecom, PuTTY etc.

##Modular Device Server

###Firmware for Arduino-like Devices

README files in examples directory of the ModularServer firmware
repository are a good place to start reading for more details on
interacting with modular devices.

[ModularServer](https://github.com/janelia-arduino/ModularServer)

##Modular Device Client

###Serial Terminal

[Serial Terminal](https://github.com/janelia-modular-devices/modular_device_serial_terminal.git)

Example Method Calls

```shell
blinkLed 0.5 0.5 10
getLedPin
```

###Python

[modular_client_python](https://github.com/janelia-pypi/modular_client_python.git)

Example Method Calls

```python
dev.blink_led(0.5,0.5,10)
led_pin = dev.get_led_pin()
```

###Matlab

[modular_client_matlab](https://github.com/janelia-matlab/modular_client_matlab.git)

Example Method Calls

```matlab
dev.blinkLed(0.5,0.5,10)
led_pin = dev.getLedPin()
```

###Arduino

[ModularClient](https://github.com/janelia-arduino/ModularClient.git)

Example Method Calls

```c++
dev.callServerMethod("blinkLed",0.5,0.5,10);
long led_pin = dev.callServerMethod("getLedPin");
```

###Labview

[modular_client_labview](https://github.com/janelia-labview/modular_client_labview.git)

##Modular Device Hardware Part Numbers

[part_numbers](./part_numbers.csv)

##Git

<https://github.com/janelia-idf/git_setup>

Note that this repository contains submodules. After cloning this
repository, run these commands to fetch the data from the submodules:

```shell
git submodule init
git submodule update
```
