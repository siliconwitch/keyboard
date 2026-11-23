# Design decisions

Decisions not yet recorded in firmware code or KiCad files.

## Switches

- Kailh Choc v1 (PG1350).
- Key pitch: 18 mm horizontal, 17 mm vertical, the usual Choc v1 spacing. The 17 × 16 mm printed caps leave a 1 mm gap each way.

## Layout

- Key tops sit 10 mm above the top board, measured with the printed caps.
- The battery, a flat pouch cell of about 4 × 40 × 45 mm, sits on the board under the touchpad. The force sensors, actuators and drivers sit beside it.
- The battery area is a section held by mouse bites. Breaking it out of the top board gives a pocket 1.6 mm deeper for a thicker cell. The section has no copper on any layer, and the joining holes and touchpad parts stay outside it.
- The controller, PMIC, USB-C connector and antenna go in the back-right corner, around the touchpad and battery. The space left of the bottom-row Alt is the fallback, as drawn in `docs/layout.svg`.

## Touchpad

- Touch sensor: Azoteq TPS65-201A-S, 65 × 49 mm, IQS550 controller. I2C at 7-bit address 0x74, plus RDY and NRST lines.
- Force sensing: one Alps Alpine HSFPAR under each corner of the touchpad, soldered to the top board.
- Haptic actuators: two Vybronics VL120628H linear resonant actuators.
- Haptic drivers: one TI DRV2605L per actuator, on the top board. The DRV2605L address is fixed at 0x5A, so each sits on its own I2C bus.

## Controller and power

- SoC: Nordic nRF54LM20A with a 32 MHz crystal and a 32.768 kHz crystal.
- PMIC: Nordic nPM1300.
- Antenna: Ignion NN02-101 in a board corner, with a 5 × 5 mm copper-free area on every layer and a pi matching network tuned with a VNA.
- USB-C connector for charging and firmware updates.
- The two DRV2605L drivers run from VSYS with no load switch. Holding EN low shuts each down to 4 µA (7 µA max). If VSYS can exceed the DRV2605L's 5.2 V limit on USB power, they run from the battery instead.
- The nPM1300's two load switches stay free for other loads.

## Chassis

- Both boards come from the same Gerbers. Clamp them together and solder each switch pin through both, so the solder joins the pin and both boards.
- Switch pin holes are only slightly larger than the standard Choc footprint. A tight gap lets solder climb the full 3.2 mm.
- Pads connected to a copper pour use thermal relief spokes.
- The bottom layer has no exposed copper except through-hole pads. This stops pads on the bottom board's top face from shorting to the top board.
- Extra plated holes, filled with solder or short wire pins, join the boards under the touchpad where there are no switch pins.
- Check both boards sit flat on glass before soldering them together.

## Firmware

- ZMK, starting from Framework's nRF54LM20A fork until main-line ZMK supports the chip.

## Space bar

- The first board carries two footprints: a full bar with one center switch and a wire stabilizer in printed brackets, and a split bar. Choose by feel after printing both.
