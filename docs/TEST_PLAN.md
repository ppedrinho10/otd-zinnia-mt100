# Test plan

## Baseline

1. Use OpenTabletDriver v0.6.7.
2. Remove or fully close the original Zinnia driver.
3. Place the local reference configuration in the OTD `Configurations` folder.
4. Reconnect the tablet and confirm it appears as `10moon 1060N`.

## Features to validate

- Cursor movement across all four corners
- Pressure range and return to zero
- Pen tip click and release
- Click-and-drag
- Side button 1
- Side button 2
- Tablet auxiliary buttons
- Tilt X/Y
- Area orientation and aspect ratio

## Required evidence for an upstream request

- OpenTabletDriver diagnostics from an uninitialized connection
- OpenTabletDriver diagnostics after the local configuration initializes the tablet
- HID report descriptor
- Exact original-driver product/version information
- Tablet debugger recording when available
- Reproducible description of every working and failing function
