# Bambulab-A1-Series-Plotter-Mod
This is a plotter mod for the Bambulab A1 and A1 Mini.
![image](https://cdn.hackclub.com/019f95e4-0116-711e-b5a8-80d8adbe2b54/IMG_6886.jpeg)
---
## Printer Profile
The custom printer profiles are currently available for the:
**BambulLab A1 Mini 0.2mm/0.4mm nozzle**
**BambulLab A1 Mini 0.2mm/0.4mm nozzle**
I created custom printer profiles, that make the printer home on the front of the print bed to avoid crashing the pen into the bed.

### Machine Start G-Code
```python
;===== date: 20260719 =====================
M104 S1
M140 S1
G90
G28 X Y ; home x/y
M104 S1
M140 S1
G1 X128 Y0 F18000 ; move toolhead to avoid pen collision
G28 Z ; home z at the new position
G92 Z0 ; reset new height to zero
M104 S1
M140 S1
M211 X0 Y0 Z0
M975 S1
```

### Machine End G-Code
```python
;===== date: 20260719 =====================
M400 ; wait for buffer to clear
G92 E0 ; zero the extruder
G90

G1 Z{max_layer_z + 50} F600 ; lower z a little

G1 X0 Y200 F6000 ; move toolhead to the left

M140 S0 ; turn off bed
M104 S0 ; turn off hotend
M106 S0 ; turn off part cooler 
M106 P2 S0 ; turn off remote cooler
M106 P3 S0

M220 S100
M201.2 K1.0
M73.2 R1.0

M400
M18 X Y Z
```
---
## Filament Profile

The custom filament profile avoids nozzle and print bed heating and fan cooling during the print.
For the Plot the model should be set to only one layer.

To prevent pen strokes set the Z-Hop int the filament settings under **Settings Overrides > Retraction** between 0.5-1mm and the Z-Hop Type to automatic
