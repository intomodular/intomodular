# Developing a Teensy eurorack module.

## Problems!

### Problem #1 - Can eurorack power a Teensy board?

Yes! It can. The Eurorack cables protocol have a +12V and a -12V rail but they also provide a +5V rail that can be used to power your Teensy board. Please be aware that in order to power a Teensy board we would need to use the Vin input. So be sure that your Teensy board has a Vin input that translate voltages into a suitable 3.3V.

Below, a simple definition of signals that travel through a eurorack 16 pins ribbon cable:

```
16 PINS
+-----------+
| [16] [15] | ⇢⇢ GATE
| [14] [13] | ⇢⇢ CV
| [12] [11] | ⇢⇢ +5V
| [10] [09]|  ⇢⇢ +12V
| [08] [07]|  ⇢⇢ GND
| [06] [05] | ⇢⇢ GND
| [04] [03] | ⇢⇢ GND
| [02] [01] | ⇢⇢ -12V
+-----------+
```

And this would be the signal path for a 10 pins cable:

```
10 PINS
+-----------+
| [10] [09] | ⇢⇢ +12V
| [08] [07] | ⇢⇢ GND
| [06] [05]|  ⇢⇢ GND
| [04] [03] | ⇢⇢ GND
| [02] [01] | ⇢⇢ -12V
+-----------+
```

As you could imagine, some of the eurorak modules don't need access to the +5V pin. As for the Gate and CV pins, for what I have seen, they are hardly used.

### Problem #2 - Can Teensy output eurorack compatible voltages?

The answer is no and yes :) Eurorack standards require a -5V / +5V range or 0 / 10V range.
In the best case, Teensy can output from 0 to 5V. In some scenarios this could be enough, but if the intention is to control another module with a 1V/octave resolution, than Teensy may be missing out some of the playable notes. This can be however solved quite easily with an Op Amp. Details on how to achieve this will follow soon.

### Problem #3 - Can Teensy receive inputs from eurorack modules?

The answer is sadly no and yes :). Some Teensy variations (the 5V tolerant ones) can receive voltages up to 5V. This wouldn't cover (and actually the board would be at risk of damage) the full range of eurorack voltages. Luckily the Op Amp can also function on the opposite way and lower the input voltages to a suitable 0 to 3.3V range.
