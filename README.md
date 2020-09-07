PowerBoard Redux

These are the Eage CAD Schematics and Board files, plus the Gerbers of some boards as-built, of an AdaFruit PowerBoost 1000C (https://www.adafruit.com/product/2465) adapted to the Raspberry Pi Zero form factor. It provides power to the +5VDC pins of the RPi header (protected via Zener diode). 

Te board patches the Low Battery (LBO) signal to the Pi via a level shifter, and also adds a programmable tactile button and LED.  You can use either one of those ubiquitous square tactile / momentary buttons, or one that mounts vertically (https://www.digikey.com/product-detail/en/te-connectivity-alcoswitch-switches/1825027-5/450-1662-ND/529484). The footprints for the two buttons overlap, which looks ugly and means you really can choose only one. It also provides a spot for a vertical slide switch that enables or disables the power circuit (https://www.digikey.com/product-detail/en/c-k/OS102011MA1QN1/CKN9559-ND/1981430). It's possible to find horizontal slide switch that fits in the same footprint. (I've only ordered them from ebay.)

Python software that works with the LBO signal, button, and LED will be linked here when they are published.

The MicroUSB connector is not the same foot print as AdaFruit uses in their PowerBoost, because I couldn't figure out which one it was. The part I use is an amphenol 10118194-0001LF (https://www.digikey.com/product-detail/en/amphenol-icc-fci/10118194-0001LF/609-4618-1-ND/2785382). It still has 4 through-hole-ish studs for strength (but can be hot-air reflowed) like AdaFruit's part, but the location of the studs are incompatible.

Changelog
- Before v1.0 / Redux, I didn't know what I was doing, and kept laying out boards with traces that were way too small for the currents involved. 
- v1.01: Thickened VBAT, VLIPO, and USB traces from circuit to aux header; added zener diode to 5V trace into RPi; using VBAT rather than VLIPO in ENABLE pin switch. 

TODO:
- do over that preserve original PowerBoost footprint so that you can either reflow the board or just pop one of AdaFruit's board onto it. 

Raspberry Pi Pins used:

    GPIO17/Phy11 is connected to a momentary / tactile switch. Available for arbitrary software control (typically running my powerboard.py and associated code).
    GPIO27/Phy13 is connected to a resistor and then an LED. Available for arbitrary software control (e.g. flashing to show grace period, and typically running my powerboard.py and associated code).
    GPIO26/Phy37 is connected to via transistor and appropriate hold up resistor to the LBO signal of the PowerBoost circuit. This is how the Raspberry Pi knows to shut down. The signal is held at battery level (but level shifted to 3.3 V before hitting the RPi) until the Li Ion battery level drops below 3.4VDC (or maybe it's 3.2V, I forget) at which point the LBO signal drops to ground. This tells the software on the RPi to do a graceful shutdown.

