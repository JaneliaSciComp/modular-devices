#modular-devices

Authors:

    Peter Polidoro <polidorop@janelia.hhmi.org>

License:

    BSD

Note that this repository contains submodules. After cloning this
repository, run these commands to fetch the data from the submodules:

```shell
git submodule init
git submodule update
```

##Introduction

Modular devices are computers or electronics with microprocessors that
implement the modular device interface in software or
firmware. Modular devices have methods that can be executed locally
through a standalone interface or remotely over a communication bus
with a client/server architecture.

Modular devices can be both clients and servers and devices
communicate with one another using [JSON](http://www.json.org/)
strings. Any communication channel capable of sending and receiving
JSON strings can used to connect modular devices to each other.

Modular devices implemented on Arduino-like boards and
processors communicate over serial UART channels. Arduino-like modular
devices can connect to each other's UART channels and call each
other's methods. Host computers such as desktops, laptops, and
Raspberry Pi-like single board computers can communicate to an
Arduino-like modular device using a USB serial port.

Any programming language capable of processing JSON strings and
sending and receiving them over a serial port can be used as a client
to call methods on an Arduino-like modular device server. Or users can
interact with remote modular devices over a serial port using simple
serial terminals, such as the Arduino IDE serial monitor, cutecom,
etc.

##Firmware

README files in examples directory of the ModularDevice firmware
repository are a great place to start reading...

[ModularDevice](https://github.com/janelia-arduino/ModularDevice)

[StandaloneInterface](https://github.com/janelia-arduino/StandaloneInterface)

##Host Computer Interface

Setup host computer environment following the
[Arduino Getting Started](https://www.arduino.cc/en/Guide/HomePage)
instructions for your operating system.

###Arduino IDE

Connect a USB cable from the host computer to the modular device. Open
the Arduino IDE and select the appropriate serial port. Open the
Arduino IDE Serial Monitor and select "Newline" and "9600 baud". Type
a question mark ? into the input field and press Enter or click Send
to get started.

###Cutecom

Connect a USB cable from the host computer to the modular device. Open
cutecom and enter the appropriate serial port. Select 9600, 8, 1,
NONE, no handshake, and open for both reading and writing. Select LF
line end. Open device. Type a question mark ? into the input field
and press Enter to get started.

###Python

<https://github.com/janelia-pypi/modular_device_python.git>

###Matlab

<https://github.com/janelia-modular-devices/modular_device_matlab.git>

###NodeJS

<https://github.com/janelia-modular-devices/modular_device_nodejs.git>

##Additional Documentation

[Standalone Interface](./documentation/standalone/)

##Enclosure and Assembly Instructions

[Enclosure](https://github.com/janelia-modular-devices/modular_device_enclosure.git)

##Modular Devices

[aalborg_mfc_interface](https://github.com/janelia-modular-devices/aalborg_mfc_interface.git)

[power_switch_controller](https://github.com/janelia-modular-devices/power_switch_controller)

[mixed_signal_controller](https://github.com/janelia-modular-devices/mixed_signal_controller.git)

[pwm_controller](https://github.com/janelia-modular-devices/pwm_controller.git)

[stepper_controller](https://github.com/janelia-modular-devices/stepper_controller.git)

[audio_controller](https://github.com/janelia-modular-devices/audio_controller.git)

##Modular Device Model Numbers

[model_numbers](./model_numbers.csv)
