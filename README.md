# OpenPinMarker

An open device that measures where the pin is. Clip it to the flagstick,
hold the flag straight and press the button: the pin position is measured
to within 20 centimetres and goes to [OpenPinsheet](https://openpinsheet.com),
the open record of pin positions.

> [!NOTE]
> **Concept, October 2026. Nobody has built one yet.** Parts, prices and
> accuracy come from datasheets, published tests and the correction
> services' own targets, not from our measurements. A pilot in 2027 checks
> them on real greens.

## How it works

The flagstick centres itself in the cup, so a marker clipped just under the
flag sits over the middle of it. Whoever holds the flag keeps a bubble level
centred; a lean of two degrees moves the antenna five centimetres at one and
a half metres. One press, and a few seconds later the phone buzzes once:
saved. Three buzzes mean no position yet.

A receiver with its own antenna and correction data gets within 20
centimetres on the day. Afterwards, the raw data recorded during the round
are worked out again against a reference station, to a few centimetres.
Phones stay at about two metres.

[docs/measuring.md](docs/measuring.md) describes a round, with the flag and
with a pole from the bag.

## Two builds

The recommended build needs no base station, no internet on the course and
no subscription. The cheap build needs a free real-time correction network,
or waits for the calculation afterwards.

| | Recommended | Cheap |
|---|---|---|
| Receiver | u-blox ZED-X20P-01B, the X20 variant with Galileo HAS | Quectel LG290P class (L1, L2, L5, E6) |
| Antenna | All-band, including E6 | Helical, L1, L2 and L5 |
| Corrections on the day | Galileo HAS, from the satellite | A free network such as SAPOS, or none |
| Expected on the day | under 20 cm after settling | 1 to 2 cm with a network, about 1.5 m without |

Both share the rest: an ESP32-C3 controller that talks to the phone over
Wi-Fi, a microSD card for the raw data, one 18650 cell charged over USB-C, a
printed case with a bubble level and a 5/8-inch survey thread, and a clamp
for poles of 12 to 25 mm.

Every part with its number, source and price is in
[hardware/bom.csv](hardware/bom.csv).

## Corrections

**On the day.** Galileo's High Accuracy Service sends corrections worldwide
and free of charge. The receiver needs five to ten minutes to settle, so it
goes on in the shed and stays on for the round.

**Afterwards.** The marker logs raw satellite data all round. They are
worked out again against a reference station from daily files that many
countries publish free of charge: SWEPOS in Sweden, CORS in the US, SAPOS in
most German states. Against a station a few kilometres away, the expected
result is under 5 cm.

## What is here

| Path | What it holds |
|---|---|
| [hardware/](hardware/) | Bill of materials; case, clamp and wiring once drawn |
| [firmware/](firmware/) | Firmware for the controller, once written |
| [docs/](docs/) | How to measure, and the pilot results later |

## Status

| Part | Status |
|---|---|
| Parts list | drafted from datasheets, not ordered |
| Case and clamp | not drawn |
| Wiring | not drawn |
| Firmware | not written |
| Accuracy on a green | not measured |

## Build at your own risk

This is a design for people who build their own device. It carries no CE
marking, and nobody guarantees its accuracy. Whoever sells finished devices
becomes their manufacturer under EU law, with the duties that come with it.
The device is radio equipment; follow the radio rules of your country.

## Licences

- Firmware: GNU General Public License v3.0 or later
- Hardware (CAD, printable files, wiring, bill of materials): CERN Open
  Hardware Licence v2, Strongly Reciprocal
- Documentation and images: Creative Commons Attribution-ShareAlike 4.0

The firmware is licensed on its own, independent of the hardware.
[LICENSE](LICENSE) says which part falls under which licence; the texts are
in [LICENSES/](LICENSES/). Drawings made from the CAD go into
`docs/drawings/` and fall under the hardware licence. The pin positions a marker reports belong to
OpenPinsheet and stand under the Open Database License.
