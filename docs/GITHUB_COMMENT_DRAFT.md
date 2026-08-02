# Draft update for OpenTabletDriver issue #4301

I tested the same hardware on Windows with OpenTabletDriver v0.6.7:

- Device: Zinnia Momentum MT100 / SZ PING-IT INC. T505 Graphic Tablet
- VID:PID: 08F2:6811
- A local configuration based on the old 10moon 1060N definition initializes and detects the device.
- Cursor movement works.
- Pressure values change normally.
- The pen tip does not generate TipDown/click.
- Pen side-button states are visible in Tablet Debugger, but behavior still needs precise validation.

I can provide:
- Windows diagnostics before and after initialization
- HID report descriptor
- Tablet Debugger screenshots
- Further hardware tests

I understand issue #4345 blocks a normal configuration because multiple 10moons devices can appear identical. I am available to test any probing method or experimental build intended to distinguish the T505.
