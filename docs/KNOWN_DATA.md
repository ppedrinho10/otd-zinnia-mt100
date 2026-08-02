# Known device data

## USB interfaces

Main digitizer interface:
- VID: 2290 (`0x08F2`)
- PID: 26641 (`0x6811`)
- Input report length: 64

Auxiliary interface:
- Input report length: 8
- Output report length: 9
- Feature report length: 8

## HID-mode values

- X maximum: 32767
- Y maximum: 32767
- Pressure maximum: 2047
- Tilt X: -127..127
- Tilt Y: -127..127

## Reference configuration assumptions

The copied `1060N-reference.json` uses:
- `TenMoonReportParser`
- MaxX/MaxY 4095
- MaxPressure 8191
- 12 auxiliary buttons

Those values belong to the reference 1060N configuration and must not automatically be treated as correct specifications for the T505.
