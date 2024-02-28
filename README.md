# mk19-pcb
The antithesis of 'keep it simple, stupid' - all the features, all the time.

Do you need...
- To use the [Cyboard flex-pcb system](https://www.cyboard.digital/product-page/dactyl-flex-pcbs)?  [and extend it?](https://github.com/christrotter/macropad-pcb)?
- Two [Ultrafalcons](https://github.com/christrotter/ultrafalcon)...per side?
- SPI devices
  - PMW3360/3389 (_right side only_)
  - Dual GC9A01 TFTs per side
  - Quad-shift register-powered 32 pins for rows/cols? ([available as a dedicated breakout here](https://github.com/christrotter/shift-register-spi-breakout-pcb))
- [5-way switch](https://github.com/christrotter/5way-pcb) or [RKJXT](https://github.com/christrotter/rkjxt-mini-breakout) for arrow keys?
- Perhaps enough RGB to illumine your entire home? (_and almost certainly require 5v supplementary power - a feature, not a bug!_)  
- Audio and ADC breakouts?  Reset switch? Power and debug breakouts?
- And use an existing RP Pico to do it?

...probably not, which is why I had to design my own pcb.  So here it is...

<img src="images/arcboardinator.jpg" width="800"/>

<img src="images/pcb-3d.jpg" width="800"/>

# the community that built it
- burkfers (research assistant extraordinaire)
- bomtarnes, chefcooke, walrus, wimads, yingeling, genki, others for design/3d printing help
- Quentin @ BKB & Erik @ Cyboard
- casuanoob (Falcon and diy pcb inspiration)
- tzarc, freznel, KarlK90, Dr. Faustroll, GeorgeN, (and others!) work on shift registers, pcbs, etc
- BKB discord crew; QMK discord; fingerpunch discord (Sadek and Melon, thanks!)
- cardiactuna for the font suggestion

# rev2 improvements
- added rkjxt to dpad connector
- added resistor networks for col shift register pulldown
- relocated cyboard connectors
- fixed a bunch of incorrect pinout orderings
- changed from solder pads to pin jumpers
- re-thought led bypass
- moved TFTs to FFC cables, made 3 of them
- added external 5v power source option
- re-thought the test pins

# design goals
- Provide a re-usable platform for the arcboards
- Make it possible to use the Cyboard flex-pcb system to save on the madness of per-key pcb soldering
- Minimize GPIO usage by moving cols/rows over to shift registers
- Reduce the amount of fiddly soldering and wire stripping a normal hand-wire build requires of you
- USB-C interconnects
- General improvements on the mk17 as a whole

## feature details
- Raspberry PI Pico (RP2040) footprint - just add pin headers and solder away - or, solder directly to pads
- keys provided through the [Cyboard flex-pcb system](https://www.cyboard.digital/product-page/dactyl-flex-pcbs) or, JST-XH 2.54 headers
- macropad using Cyboard flex-pcb keys, custom breakout pcb: https://github.com/christrotter/macropad-pcb (0.5mm pitch 16-pin FFC cable)
  - in future I'd just make this a custom FPC cable
- dpad using custom breakout pcbs [5-way switch](https://github.com/christrotter/5way-pcb) or [RKJXT](https://github.com/christrotter/rkjxt-mini-breakout)
 - diodes are configured for ROW2COL (_to match Cyboard_)
- USB-C split connector w. tzarc-grade voltage protection
 - included a solder pad jumper to bypass if needed
- split-handedness via pin (jumper)
- SPI breakouts
  - PMW33xx
  - 3x TFT LCD (e.g. GC9A01)
  - shift registers (595 for rows, 589 for cols)
- pin breakouts
 - power, debug, ADC, audio, reset
 - remaining GPIO pins
 - test points
- led breakouts w. bypasses
 - keys
 - 2x falcon pcbs
 - indicator strip
 - screen-mounted external indicators via USB-C
  - this passes 5v/GND, level-shifted 5v LED DI/DO signal via USB-C cable
 - pin for whatever else you want to add to the chain

## pcb features
<img src="images/pcb-overview.jpg" width="1200"/>

- two-layer pcb w. dual ground planes tied w. vias
- components configured as per datasheets
- bypass capacitors!
- care taken to avoid power running alongside signal for too long

<img src="images/pcb-3d.jpg" width="1200"/>

# schematic overview
## mcu
<img src="images/sch-mcu-headers.jpg" width="1200"/>

## keys via shift registers
<img src="images/sch-rows_cols.jpg" width="1200"/>
<img src="images/pcb-rows-shiftreg.jpg" width="1200"/>
<img src="images/pcb-cols-shiftreg.jpg" width="1200"/>
<img src="images/pcb-cyboard-breakouts.jpg" width="1200"/>

## peripherals
<img src="images/sch-peripherals.jpg" width="1200"/>

## usb connections
<img src="images/sch-split-connector.jpg" width="1200"/>
<img src="images/pcb-split-power.jpg" width="1200"/>

## breakouts
<img src="images/sch-breakouts.jpg" width="1200"/>
<img src="images/sch-leds.jpg" width="1200"/>
<img src="images/sch-gc9a01-lcds.jpg" width="1200"/>