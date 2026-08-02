# OpenTabletDriver support research — Zinnia Momentum MT100 / T505

Community research project for the **Zinnia Momentum MT100**, internally identified as **SZ PING-IT INC. T505 Graphic Tablet**.

## Device

- USB VID:PID: `08F2:6811`
- Internal name: `T505 Graphic Tablet`
- OpenTabletDriver tested: `v0.6.7`
- Known working base configuration: `10moon 1060N`

## Current test status

- Detection: working with the local 1060N configuration
- Pen movement: working
- Pressure: working
- Pen tip click: not working
- Pen side buttons: detected, but current bindings/interpretation need validation
- Tablet buttons: not yet fully validated

## Important limitation

Several different “10moons” tablets can expose the same USB VID/PID. The official OpenTabletDriver project currently tracks this as a device-identification blocker. Therefore this repository must not claim broad compatibility until the T505 can be distinguished reliably.

## Contributors

- Hardware testing, HID information and validation: **Pedro Paulo Lima**

## Next technical objective

Capture or derive a reliable T505-specific identification method and verify how `TipDown` is encoded after vendor-mode initialization. Avoid submitting a parser based only on `Pressure > 0` until click/release behavior and low-pressure edge cases are tested.

## Acknowledgements

This research builds upon the previous investigation published in the
OpenTabletDriver project issue #4301.

Special thanks to GitHub user @zondonaidejr for publishing the initial
T505 investigation, diagnostics and the 1060N configuration that made
this research possible.
