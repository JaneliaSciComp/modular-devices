#Modular Device

Authors:

    Peter Polidoro <polidorop@janelia.hhmi.org>

License:

    BSD

##Standalone Interface

* Plug in the appropriate power supply for the modular device.

<img src="standalone_01.jpg" width="640">

* When the modular device first powers up, the blinking cursor is in
  the upper left corner. Pressing the white button will execute
  whichever method is written on the first line of the display. In
  this example, the method is toggleChannel.

<img src="standalone_02.jpg" width="640">

* In this example, pressing the white button toggles channel 0,
  turning it on if it was off and off if it was on. Note that the
  channel 0 LED is now lit.

<img src="standalone_03.jpg" width="640">

* Pressing down on the encoder button causes the blinking cursor to
  move to the next interactive variable on the display screen, if
  there is one. In this example, the channel number is an interactive
  variable, so pressing down on the encoder button once moves the
  cursor from the upper left corner (the device method interactive
  variable) to on top of the channel number. Pressing the encoder
  button again would cause the blinking cursor to jump back to the
  upper left corner again.

<img src="standalone_04.jpg" width="640">

* Turning the encoder knob causes the interactive variable underneath
  the blinking cursor to change.

<img src="standalone_05.jpg" width="640">

* Pressing the white button still causes the method on the top of the
  screen to execute, but with the new interactive variable values. In
  this example, pressing the white button causes LED 3 to light.

<img src="standalone_06.jpg" width="640">

* Press the encoder button again to change the current interactive
  variable back to the device method (the blinking cursor back in the
  upper left corner of the screen).

<img src="standalone_07.jpg" width="640">

* Now when you turn the encoder knob, the device method changes. In
  this example, the device method changed to setAllChannelsOn.

<img src="standalone_08.jpg" width="640">

* Again, pressing the white button causes the current device method to
  execute.

<img src="standalone_09.jpg" width="640">

* All channels turn on and all LEDs are lit.

<img src="standalone_10.jpg" width="640">

* The LEDs are useful for debugging, but some experiments require
  darkness so every modular device comes with a light switch.

<img src="standalone_11.jpg" width="640">

* Flipping the light switch turns the lights off, even though all of
  the channels are still on. The display still shows the text, but the
  display light is off making it more difficult to read.

<img src="standalone_12.jpg" width="640">

* Every modular device has a different set of methods and the methods
  exposed by the standalone interface are not necessarily the same as
  those exposed by the host computer interface over USB. The buttons
  and knobs work the same way for every modular device however.
