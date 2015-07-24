modular-devices
===============

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

##Host Computer Interface

[Python](https://github.com/janelia-modular-devices/modular_device_python)

[Matlab](https://github.com/janelia-modular-devices/modular_device_matlab)

[NodeJS](https://github.com/janelia-modular-devices/modular_device_nodejs)

###Arduino Serial Monitor

Open the Serial Monitor in the Arduino IDE.

Set the baud rate to 9600.

Set the line ending to 'Newline'.

To get help information about the modular device, type a single
question mark ? into the input field and press the 'Send' button or
press the 'Enter' key.

```shell
?
```

The response will contain a field named "methods", which is an array
of user methods. To execute a method, simply type it into the input
field and press the 'Send' button or press the 'Enter' key.

Example Method:

```shell
getLedsPowered
```

Example Response:

```json
{
  "method":"getLedsPowered",
  "leds_powered":true,
  "status":success
}
```

Example Method with Parameters:

```shell
setSerialNumber
```

Example Response:

```json
{
  "method":"setSerialNumber",
  "status":error,
  "error_message":"Incorrect number of parameters. 0 given. 1 needed."
}
```

To get more information about a single method, enter the method
followed by a question mark '?'.

Example Method Help:

```shell
setSerialNumber ?
```

Example Response:

```json
{
  "method":"setSerialNumber",
  "parameters":[
    "serial_number"
  ],
  "status":success
}
```

To get more verbose help about the method, including more information
about the parameters each method takes, type the method name followed
by two questions marks '??'.

Example Method Verbose Help:

```shell
setSerialNumber ??
```

Example Response:

```json
{
  "method":"setSerialNumber",
  "parameters":[
    {
      "serial_number":{
        "type":"long",
        "min":0,
        "max":65535
      }
    }
  ],
  "status":success
}
```

Example Method:

```shell
setSerialNumber 32
```

Example Response:

```json
{
  "method":"setSerialNumber",
  "status":success
}
```

The serial number setting persists even after the device is powered
off. The serial number is used to differentiate several identical
devices connected to a single host machine at one time.

To reset the serial number to the default value, use the resetDefaults
method.

Example Method:

```shell
resetDefaults
```

Example Response:

```json
{
  "method":"resetDefaults",
  "status":success
}
```

To get more verbose help, including information about the parameters
each method takes, type two questions marks:

```shell
??
```

##Arduino Firmware

<https://github.com/janelia-modular-devices/modular_device_arduino>

##Enclosure

<https://github.com/janelia-modular-devices/modular_device_enclosure>
