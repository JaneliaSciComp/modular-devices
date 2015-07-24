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

To get more verbose help, including information about the parameters
each method takes, type two questions marks:

```shell
??
```

To get more information about a single method, enter the method
followed by a question mark '?'.

Example Method Help:

```shell
setSerialNumber ?
```

To get more verbose help about the method, including more information
about the parameters each method takes, type the method name followed
by two questions marks '??'.

Example Method Verbose Help:

```shell
setSerialNumber ??
```

##Arduino Firmware

<https://github.com/janelia-modular-devices/modular_device_arduino>

##Enclosure

<https://github.com/janelia-modular-devices/modular_device_enclosure>
