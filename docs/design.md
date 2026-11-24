# Design decisions

Decisions not yet recorded in firmware code or KiCad files.

## Switches

- The switches form a key matrix with one 1N4148W diode (Diodes Inc. 1N4148W-7-F, SOD-123) per switch, hand soldered.

## Layout

- Key tops sit 10 mm above the top board, measured with the printed caps.
- The battery, a flat pouch cell of about 4 × 40 × 45 mm, sits on the board under the touchpad. The force sensors, actuators and drivers sit beside it.
- The battery area is a section held by mouse bites. Breaking it out of the top board gives a pocket 1.6 mm deeper for a thicker cell. The section has no copper on any layer, and the joining holes and touchpad parts stay outside it.
- The controller, PMIC, USB-C connector and antenna go in the back-right corner, around the touchpad and battery. The space left of the bottom-row Alt is the fallback, as drawn in `docs/layout.svg`.

## Touchpad

- Touch sensor: Azoteq TPS65-201A-S, 65 × 49 mm, IQS550 controller. I2C at 7-bit address 0x74, plus RDY and NRST lines.
- Wires join the touchpad module to six solder pads on the top board. The board has no FPC connector.
- Force sensing: one Alps Alpine HSFPAR under each corner of the touchpad, soldered to the top board.

## Controller and power

- Antenna: Ignion NN02-101 in a board corner, with a 5 × 5 mm copper-free area on every layer and a pi matching network tuned with a VNA.
- USB-C connector for charging and firmware updates: GCT USB4105-GF-A, USB 2.0, top mount. Its 0.95 mm shell stakes stay inside the top board.

## Chassis

- Both boards come from the same Gerbers. Clamp them together and solder each switch pin through both, so the solder joins the pin and both boards.
- Switch pin holes are only slightly larger than the standard Choc footprint. A tight gap lets solder climb the full 3.2 mm.
- Pads connected to a copper pour use thermal relief spokes.
- The bottom layer has no exposed copper except through-hole pads. This stops pads on the bottom board's top face from shorting to the top board.
- Extra plated holes, filled with solder or short wire pins, join the boards under the touchpad where there are no switch pins.
- Check both boards sit flat on glass before soldering them together.

## Firmware

- ZMK, starting from Framework's nRF54LM20A fork until main-line ZMK supports the chip.
