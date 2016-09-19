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

[StandaloneInterface](https://github.com/janelia-arduino/StandaloneInterface)

####Instructions for the Arduino Libraries Necessary to Compile the Firmware

[arduino-libraries](https://github.com/janelia-arduino/arduino-libraries)

###Example Server API

```json
{
  "id":"??",
  "result":{
    "device_info":{
      "device_name":"modular_server",
      "firmware_name":"field_tester",
      "firmware_version":{
        "major":0,
        "minor":1,
        "patch":0
      },
      "hardware_name":"",
      "model_number":0,
      "processor":"mega",
      "serial_number":0
    },
    "methods":[
      {
        "name":"getMemoryFree",
        "parameters":[],
        "result_type":"long"
      },
      {
        "name":"getFieldDefaultValues",
        "parameters":[],
        "result_type":null
      },
      {
        "name":"setFieldsToDefaults",
        "parameters":[],
        "result_type":null
      },
      {
        "name":"setFieldToDefault",
        "parameters":[
          "field_name"
        ],
        "result_type":null
      },
      {
        "name":"getFieldValues",
        "parameters":[],
        "result_type":"object"
      },
      {
        "name":"getFieldValue",
        "parameters":[
          "field_name"
        ],
        "result_type":"value"
      },
      {
        "name":"getFieldElementValue",
        "parameters":[
          "field_name",
          "field_element_index"
        ],
        "result_type":"value"
      },
      {
        "name":"setFieldValue",
        "parameters":[
          "field_name",
          "field_value"
        ],
        "result_type":null
      },
      {
        "name":"setFieldElementValue",
        "parameters":[
          "field_name",
          "field_element_index",
          "field_value"
        ],
        "result_type":null
      },
      {
        "name":"setAllFieldElementValues",
        "parameters":[
          "field_name",
          "field_value"
        ],
        "result_type":null
      },
      {
        "name":"getDoubled",
        "parameters":[],
        "result_type":"double"
      },
      {
        "name":"getBool",
        "parameters":[],
        "result_type":"bool"
      },
      {
        "name":"getLongArrayFixed",
        "parameters":[],
        "result_type":"array"
      },
      {
        "name":"getLongArrayVariable",
        "parameters":[],
        "result_type":"array"
      },
      {
        "name":"setLongArrayFixed",
        "parameters":[],
        "result_type":"bool"
      },
      {
        "name":"setLongArrayVariable",
        "parameters":[],
        "result_type":"bool"
      },
      {
        "name":"setLongArrayParameter",
        "parameters":[
          "long_array_parameter"
        ],
        "result_type":"bool"
      },
      {
        "name":"getStringAll",
        "parameters":[],
        "result_type":"string"
      },
      {
        "name":"getStringSome",
        "parameters":[
          "length_parameter"
        ],
        "result_type":"string"
      },
      {
        "name":"getCount",
        "parameters":[
          "count"
        ],
        "result_type":"string"
      },
      {
        "name":"getCountArray",
        "parameters":[
          "count_array"
        ],
        "result_type":"array"
      },
      {
        "name":"getDirection",
        "parameters":[
          "direction"
        ],
        "result_type":"string"
      },
      {
        "name":"getDirectionArray",
        "parameters":[
          "direction_array"
        ],
        "result_type":"array"
      },
      {
        "name":"checkMode",
        "parameters":[],
        "result_type":"string"
      },
      {
        "name":"incrementMode",
        "parameters":[],
        "result_type":"string"
      }
    ],
    "parameters":[
      {
        "name":"field_name",
        "type":"string"
      },
      {
        "name":"field_value",
        "type":"value"
      },
      {
        "name":"field_element_index",
        "type":"long"
      },
      {
        "name":"long_array_parameter",
        "type":"array",
        "array_element_type":"long"
      },
      {
        "name":"length_parameter",
        "type":"long",
        "min":0,
        "max":20
      },
      {
        "name":"count",
        "type":"long",
        "subset":[
          10,
          20,
          30,
          40,
          50,
          60,
          70
        ]
      },
      {
        "name":"count_array",
        "type":"array",
        "array_element_type":"long",
        "array_element_subset":[
          10,
          20,
          30,
          40,
          50,
          60,
          70
        ],
        "array_element_min":30,
        "array_element_max":60,
        "array_length_min":1,
        "array_length_max":3
      },
      {
        "name":"direction",
        "type":"string",
        "subset":[
          "UP",
          "DOWN",
          "LEFT",
          "RIGHT"
        ]
      },
      {
        "name":"direction_array",
        "type":"array",
        "array_element_type":"string",
        "array_element_subset":[
          "UP",
          "DOWN",
          "LEFT",
          "RIGHT"
        ],
        "array_length_min":2,
        "array_length_max":4
      }
    ],
    "fields":[
      {
        "name":"serial_number",
        "type":"long",
        "min":0,
        "max":65535,
        "value":0,
        "default_value":0
      },
      {
        "name":"double",
        "type":"double",
        "value":3.141590,
        "default_value":3.141590
      },
      {
        "name":"bool",
        "type":"bool",
        "value":false,
        "default_value":false
      },
      {
        "name":"long_array",
        "type":"array",
        "array_element_type":"long",
        "array_element_min":-3,
        "array_element_max":10,
        "array_length_min":1,
        "array_length_max":4,
        "value":[
          5,
          4,
          3,
          2
        ],
        "default_value":[
          5,
          4,
          3,
          2
        ]
      },
      {
        "name":"double_array",
        "type":"array",
        "array_element_type":"double",
        "array_element_min":-33.333000,
        "array_element_max":100.000000,
        "array_length_min":1,
        "array_length_max":3,
        "value":[
          -1.100000,
          2.200000,
          3.300000
        ],
        "default_value":[
          -1.100000,
          2.200000,
          3.300000
        ]
      },
      {
        "name":"bool_array",
        "type":"array",
        "array_element_type":"bool",
        "array_length_min":1,
        "array_length_max":2,
        "value":[
          false,
          true
        ],
        "default_value":[
          false,
          true
        ]
      },
      {
        "name":"string",
        "type":"string",
        "value":"abcdef",
        "default_value":"abcdef"
      },
      {
        "name":"odd",
        "type":"long",
        "subset":[
          1,
          3,
          5,
          7,
          9
        ],
        "value":5,
        "default_value":5
      },
      {
        "name":"mode",
        "type":"string",
        "subset":[
          "RISING",
          "FALLING",
          "CHANGE"
        ],
        "value":"RISING",
        "default_value":"RISING"
      }
    ]
  }
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

[Matlab](https://github.com/janelia-matlab/modular_device_matlab.git)

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

####Instructions for the Arduino Libraries Necessary to Compile the Firmware

[arduino-libraries](https://github.com/janelia-arduino/arduino-libraries)

###NodeJS

[NodeJS](https://github.com/janelia-modular-devices/modular_device_nodejs.git)

##Standalone Interface Documentation

[Standalone Interface](https://github.com/janelia-modular-devices/modular_device_standalone_interface.git)

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

##Modular Device Model Numbers

[model_numbers](./model_numbers.csv)
