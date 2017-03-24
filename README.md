# modular-devices

Authors:

    Peter Polidoro <polidorop@janelia.hhmi.org>

License:

    BSD

## Introduction

Modular devices are combinations of open source object oriented
hardware, firmware, and software.

Modular devices extend object oriented software concepts into object
oriented hardware, allowing you to create hardware objects with
methods for executing actions.

Modular device methods can be executed locally or remotely over a
communication bus or channel with a client/server architecture.

Object oriented hardware is a mixture of processors, electronics, and
mechanics for interacting with, sensing, and controlling things in the
physical world. Each hardware object can be used independently or
combined like software objects to create more complex systems. The
hardware objects can be implemented in a variety of form factors. Some
form factors might be designed to be as small an inexpensive as
possible, while others might be larger with more features or capacity,
but every object has its own processor, with one or more communication
channels and set of interrupts, and can be used on its own or combined
with any other hardware object, regardless of form factor. Hardware
objects can scale both up, by combining many of them together when
large complicated systems are needed, and scale down, so only a single
hardware object is necessary when needs are small and simple,
minimizing cost and component count.

Object oriented firmware/software server objects run on the hardware
objects and provide the interface necessary to interact with and
control the device. Each firmware/software server object adds a set of
methods and parameters to the device. Every device may consist of
several layers of firmware/software server objects. Each layer extends
or modifies the layer beneath it, like inheritance and composition in
traditional object oriented software. Lower layers may provide general
features specific to the particular hardware it is running on, while
higher layers may add features specific to the particular task the
user may want to run or hardware connected to the
device. Firmware/software server objects are written to maximize code
reuse and separation of concerns.

Object oriented firmware/software client objects may be run on other
modular devices or on host computers connected to one or more modular
devices. The client software may be written in almost any language
capable of writing strings over the communication channel to the
modular device. Only one small client software driver should be
necessary in each language to talk to all firmware and hardware
objects. When the client software object initializes, it asks the
modular devices about its methods and parameters, and then uses that
information to create the client object. So new or modified modular
devices can be connected to a client object and controlled without the
user needing to change or update the client object code. Once the
client has connected to the server, other software may interact with
the client, calling methods on the local client object that
automatically call the remote methods on the modular device over the
communication channel.

## Details

Modular devices are computers or electronics with microprocessors that
implement
the
[modular device protocol](https://github.com/janelia-modular-devices/modular_device_protocol.git) in
software or firmware.

Modular device servers consist of one or more methods that perform
some action.

Each method takes zero or more parameters to specify the
action and methods may or may not return a value. Parameters and
return values can be any JSON type, including objects with key/value
pairs, arrays with an ordered collection of values, strings, numbers,
booleans, or null.

There are three types of methods: functions, properties, and
callbacks.

Functions are the most basic method and calling them
executes their programmed action using the values of whatever
parameters it requires, if any.

Properties are methods used for getting and setting field data
permanently stored on the device. The first parameter of a property
method is a function string. Each property function takes zero or more
additional parameters. Example property functions are 'getValue',
which takes zero additional parameters and returns the stored field
value, and 'setValue', which takes one parameter, the new desired
value of the property field. Every property function returns the new
stored value of the property field. Calling a property with no
parameters is a shortcut to the property 'getValue' function.

Callbacks are methods that can be called like functions or triggered
from interrupts. When callbacks are triggered by an interrupt, they
take no parameters and return no result, instead they can potentially
use property values stored on the device like functions use
parameters. When callbacks are called from a communication channel,
the first parameter of the callback method is a function string. Each
callback function takes zero or more additional parameters. Example
callback functions are 'trigger', which takes no addtional parameters
and executes the callback action as if it had been triggered by an
interrupt, and 'attachTo', which takes two additional parameters, an
interrupt and a mode and attaches the callback to the interrupt and
sets the trigger mode. Calling a callback with no parameters is a
shortcut to the callback 'trigger' function.

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

## Modular Device Server

### Firmware for Arduino-like Devices

README files in examples directory of the ModularServer firmware
repository are a good place to start reading for more details on
interacting with modular devices.

[ModularServer](https://github.com/janelia-arduino/ModularServer)

## Modular Device Client

### Serial Terminal

[Serial Terminal](https://github.com/janelia-modular-devices/modular_device_serial_terminal.git)

Example Method Calls

```shell
blinkLed 0.5 0.5 10
getLedPin
```

### Python

[modular_client_python](https://github.com/janelia-pypi/modular_client_python.git)

Example Method Calls

```python
dev.blink_led(0.5,0.5,10)
led_pin = dev.get_led_pin()
```

### Matlab

[modular_client_matlab](https://github.com/janelia-matlab/modular_client_matlab.git)

Example Method Calls

```matlab
dev.blinkLed(0.5,0.5,10)
led_pin = dev.getLedPin()
```

### Arduino

[ModularClient](https://github.com/janelia-arduino/ModularClient.git)

Example Method Calls

```c++
dev.callServerMethod("blinkLed",0.5,0.5,10);
long led_pin = dev.callServerMethod("getLedPin");
```

### Labview

[modular_client_labview](https://github.com/janelia-labview/modular_client_labview.git)

## Modular Device Hardware Part Numbers

[part_numbers](./part_numbers.csv)

## Git

<https://github.com/janelia-idf/git_setup>

Note that this repository contains submodules. After cloning this
repository, run these commands to fetch the data from the submodules:

```shell
git submodule init
git submodule update
```

## Example API

```json
{
  "id":"??",
  "result":{
    "device_id":{
      "name":"pellet_dispenser",
      "form_factor":"3x2",
      "serial_number":0
    },
    "API":{
      "firmware":["ALL"],
      "functions":[
        "getDeviceId",
        "getDeviceInfo",
        "getInterruptInfo",
        "detachAllInterrupts",
        "getApi",
        "getApiVerbose",
        "getPropertyDefaultValues",
        "setPropertiesToDefaults",
        "getPropertyValues",
        "reinitialize",
        "enable",
        "disable",
        "enableAll",
        "disableAll",
        "enabled",
        "moveBy",
        "moveTo",
        "moveAt",
        "moveSoftlyBy",
        "moveSoftlyTo",
        "stop",
        "stopAll",
        "zero",
        "zeroAll",
        "getPositions",
        "getTargetPositions",
        "atTargetPositions",
        "getVelocities",
        "getTargetVelocities",
        "atTargetVelocities",
        "switchesActive",
        "home",
        "homing",
        "homed",
        "minimizeCurrent",
        "restoreCurrent",
        "homeStage",
        "stageHoming",
        "stageHomed",
        "moveStageTo",
        "moveStageSoftlyTo",
        "getStagePositions",
        "stageAtTargetPositions",
        "dispensePellet",
        "enableDispenser",
        "disableDispenser"
      ],
      "parameters":[
        "firmware",
        "channel",
        "position",
        "velocity",
        "stage_positions"
      ],
      "properties":[
        "serialNumber",
        "stepsPerPositionUnit",
        "velocityMax",
        "velocityMin",
        "accelerationMax",
        "enablePolarity",
        "stepPolarityInverted",
        "dirPolarityInverted",
        "switchActivePolarity",
        "leftSwitchStopEnabled",
        "rightSwitchesEnabled",
        "rightSwitchStopEnabled",
        "switchSoftStopEnabled",
        "homeVelocity",
        "currentScale",
        "microstepsPerStep",
        "stageChannelCount",
        "stagePositionMin",
        "stagePositionMax",
        "basePosition",
        "deliverPosition"
      ],
      "callbacks":[
        "deliver",
        "abort"
      ]
    }
  }
}
```

## Example Device Info

```json
{
  "id":"getDeviceInfo",
  "result":{
    "processor":"MK20DX256",
    "hardware":[
      {
        "name":"Teensy",
        "version":"3.2",
        "interrupts":[]
      },
      {
        "name":"modular_device_base",
        "part_number":1001,
        "version":"1.1",
        "interrupts":[
          "bnc_a",
          "bnc_b"
        ]
      },
      {
        "name":"step_dir_controller",
        "version":"1.0",
        "interrupts":[]
      }
    ],
    "firmware":[
      {
        "name":"ModularServer",
        "version":"2.4.0"
      },
      {
        "name":"ModularDeviceBase",
        "version":"2.2.0"
      },
      {
        "name":"StepDirController",
        "version":"1.0.0"
      },
      {
        "name":"StepperController",
        "version":"1.0.0"
      },
      {
        "name":"StageController",
        "version":"1.0.0"
      },
      {
        "name":"PelletDispenser",
        "version":"1.0.0"
      }
    ]
  }
}
```

## Example Interrupt Info

```json
{
  "id":"getInterruptInfo",
  "result":[
    {
      "name":"bnc_a",
      "hardware":"modular_device_base",
      "number":33,
      "pin":33,
      "callback":"deliver",
      "mode":"FALLING"
    },
    {
      "name":"bnc_b",
      "hardware":"modular_device_base",
      "number":32,
      "pin":32,
      "callback":"abort",
      "mode":"FALLING"
    }
  ]
}
```
