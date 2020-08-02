# Developing a Teensy eurorack module.

## Problems!

### Problem #1 - Can eurorack power a Teensy board?

Yes! It can. The Eurorack cables protocol have a +12V and a -12V rail but they also provide a +5V rail that can be used to power our Teensy board. Please be aware that in order to power a Teensy board we would need to use the Vin input rather than the 3.3V input. Also MAKE SURE that your Teensy board has a Vin input that translate voltages into a suitable 3.3V input.
