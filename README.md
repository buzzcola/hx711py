Info
----
Forked from tatobari's excellent library at https://github.com/tatobari/hx711py.

Changes
-------
Either the load cell in my $9.00 kitchen scale is janky, or the hx711 chip I obtained is jacked up, or maybe I nicked a wire hooking it all up... Whatever the cause, my readings from the hx711 were peppered with bad numbers. Some readings were off by an order of magnitude (positive or negative) while others were substantally different but close enough to mess everything up.

The result was that the original read_average() method, which should smooth out minor issues, wasn't adequate to clean up this junk.

My reimplementation of read_average is a lot more paranoid and manages to yield correct results accurate to within ~0.2g 9 times out of 10 on a 5kg load cell.

  * It defaults to 15 samples per reading instead of 3.
  * It discards the two highest and lowest readings (adjustable.)
  * It filters out anything that differs from the average by more than 20% of the standard deviation (adjustable.)

Then and only then does it return the average of results. Occasionally this means it eliminates all the readings in a set, in which case it returns None.

Instructions
------------
Check example.py to see how it works.
