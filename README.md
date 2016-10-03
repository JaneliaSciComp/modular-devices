#modular-devices

Authors:

    Peter Polidoro <polidorop@janelia.hhmi.org>

License:

    BSD

##Git

<https://github.com/janelia-idf/git_setup>

Note that this repository contains submodules. After cloning this
repository, run these commands to fetch the data from the submodules:

```shell
git submodule init
git submodule update
```

##Introduction

Modular devices extend object oriented software into object oriented
hardware, allowing you to create hardware objects with methods for
executing actions, parameters for passing information to the methods,
and fields for storing data internally.

Modular devices are computers or electronics with microprocessors that
implement the
[modular device protocol](https://github.com/janelia-modular-devices/modular_device_protocol.git)
in software or firmware. Modular devices have methods that can be
executed locally or remotely over a communication bus with a
client/server architecture.

Modular device servers consist of one or more methods that perform
some action. Each method takes zero or more parameters to specify the
action and methods may or may not return a value. Parameters and
return values can be any JSON type, including objects with key/value
pairs, arrays with an ordered collection of values, strings, numbers,
booleans, or null. Fields are used for storing data in the device.

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

####Instructions for the Arduino Libraries Necessary to Compile the Firmware

[arduino-libraries](https://github.com/janelia-arduino/arduino-libraries)

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

##Enclosure and Assembly Instructions

[Enclosure](https://github.com/janelia-modular-devices/modular_device_enclosure.git)

##Modular Devices

[modular_device_teensy](https://github.com/janelia-modular-devices/modular_device_teensy.git)

[aalborg_mfc_interface](https://github.com/janelia-modular-devices/aalborg_mfc_interface.git)

[power_switch_controller](https://github.com/janelia-modular-devices/power_switch_controller)

[mixed_signal_controller](https://github.com/janelia-modular-devices/mixed_signal_controller.git)

[pwm_controller](https://github.com/janelia-modular-devices/pwm_controller.git)

[stepper_controller](https://github.com/janelia-modular-devices/stepper_controller.git)

[audio_controller](https://github.com/janelia-modular-devices/audio_controller.git)

[led_controller](https://github.com/janelia-modular-devices/led_controller.git)

[h_bridge_controller](https://github.com/janelia-modular-devices/h_bridge_controller.git)

[encoder_interface](https://github.com/janelia-modular-devices/encoder_interface.git)

[relay_controller](https://github.com/janelia-modular-devices/relay_controller.git)

[user_interface](https://github.com/janelia-modular-devices/user_interface.git)

##Modular Device Part Numbers

[part_numbers](./part_numbers.csv)
