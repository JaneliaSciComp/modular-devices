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
implement the
[modular device interface](https://github.com/janelia-modular-devices/modular_device_interface.git)
in software or firmware. Modular devices have methods that can be
executed locally or remotely over a communication bus with a
client/server architecture.

Modular device servers consist of one or more methods that perform
some action. Each method takes zero or more parameters to specify the
action and methods may or may not return a value. Parameters and
return values can be any JSON type, including objects with key/value
pairs, arrays with an ordered collection of values, strings, numbers,
booleans, or null.

Server methods may be triggered by changes on the local device, such
as timers expiring, buttons pressed, encoders turned, or through a GUI
or command line. Alternatively, server methods may be triggered by
external sources such as TTL signals or calls from modular device
clients through communication channels.

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

[StandaloneInterface](https://github.com/janelia-arduino/StandaloneInterface)

###Example Server API

```json
{
  "device_info":{
    "name":"led_controller",
    "model_number":1001,
    "serial_number":0,
    "firmware_version":{
      "major":0,
      "minor":1,
      "patch":0
    }
  },
  "methods":[
    {
      "name":"getMemoryFree",
      "parameters":[],
      "result_type":"long"
    },
    {
      "name":"resetDefaults",
      "parameters":[],
      "result_type":null
    },
    {
      "name":"setSerialNumber",
      "parameters":[
        "serial_number"
      ],
      "result_type":null
    },
    {
      "name":"setLedOn",
      "parameters":[],
      "result_type":null
    },
    {
      "name":"setLedOff",
      "parameters":[],
      "result_type":null
    },
    {
      "name":"getLedPin",
      "parameters":[],
      "result_type":"long"
    },
    {
      "name":"blinkLed",
      "parameters":[
        "duration_on",
        "duration_off",
        "count"
      ],
      "result_type":null
    }
  ],
  "parameters":[
    {
      "name":"serial_number",
      "type":"long",
      "min":0,
      "max":65535
    },
    {
      "name":"duration_on",
      "units":"seconds",
      "type":"double",
      "min":0.100000,
      "max":2.500000
    },
    {
      "name":"duration_off",
      "units":"seconds",
      "type":"double",
      "min":0.100000,
      "max":2.500000
    },
    {
      "name":"count",
      "type":"long",
      "min":1,
      "max":100
    }
  ],
}
```

##Modular Device Client

###Serial Terminal

[Serial Terminal](https://github.com/janelia-modular-devices/modular_device_serial_terminal.git)

Example Method Calls

```shell
blinkLed 0.5 0.5 10
getLedPin
```

###Python

[Python](https://github.com/janelia-pypi/modular_device_python.git)

Example Method Calls

```python
dev.blink_led(0.5,0.5,10)
led_pin = dev.get_led_pin()
```

###Matlab

[Matlab](https://github.com/janelia-modular-devices/modular_device_matlab.git)

Example Method Calls

```matlab
dev.blinkLed(0.5,0.5,10)
led_pin = dev.getLedPin()
```

###Arduino

[ModularDevice](https://github.com/janelia-arduino/ModularDevice.git)

Example Method Calls

```c++
dev.callServerMethod("blinkLed",0.5,0.5,10);
long led_pin = dev.callServerMethod("getLedPin");
```

###NodeJS

[NodeJS](https://github.com/janelia-modular-devices/modular_device_nodejs.git)

##Standalone Interface Documentation

[Standalone Interface](https://github.com/janelia-modular-devices/modular_device_standalone_interface.git)

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
