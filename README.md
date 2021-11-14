# STSPIN32F0 OpAmp Interrupt brushless firmware
 Firmware for the stspin32f0a
 ported to an ESC I received, labeled "airfleet ver1.0 20200331dw"
 
Information I reverse engineered by looking at the layout and probing some pins and pads:
  - phase feedback coming from the motor pads:
    - 10k coming from the pad
    - 1k to ground
    - 10k to virtual center
    - virtual center goes to neg inputs of OpAmps 1, 3, and 4
  - Phase feedback to OpAmps to MCU inputs:
    - A to OpAmp3 to PF[1]
    - B to OpAmp4 to PF[0]
    - C to OpAmp1 to PA[5]
  - 10 Ohm gate resistors
  - Voltage divider VBat - 20k - PA[4] - 1k - Gnd.

There's a DCDC regulator that outputs 3.3 V, I don't know how much current it can supply.

Battery voltage range: the phase feedback dividers would be ok for 6S.

2 stacked 1 mOhm shunts for current sensing between ground and the power FETs' source connections. It's definitely connected to the overcurrent comparator (OC_comp) with a 4k7 resistor. There's also something going on with OpAmp2, but I didn't find any direct connection between OpAmp2's output and any other pin.
