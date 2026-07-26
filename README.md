# Bambulab-A1-Series-Plotter-Mod
This is a plotter mod for the Bambulab A1 and A1 Mini. The mod is based on custom printer & filament profiles and the physical tool head cover with pen mount.
![image](https://cdn.hackclub.com/019f9ae2-a48f-7247-aa75-3a4e60090c52/Cover.jpg)

---
# Hardware
There are two versions of the toolhead attachment module.

<img src="https://cdn.hackclub.com/019f9fe4-9a5b-7a24-9fc3-9e50ec578871/ToolheadAttachment.png" alt="Alt Text" width="451" height="730">
<img src="https://cdn.hackclub.com/019f9fe4-b03f-7236-90ab-b7311c1dda09/ToolheadAttachmentSpring.png" alt="Alt Text" width="451" height="730">

---
# Software
## Printer Profile
The custom printer profiles are currently available for the:
| Printer        | 0.2mm | 0.4mm | 0.6mm | 0.8mm |
| --------------- |:-----:| -----:| -----:| -----:|
| BambuLab A1 Mini|  ✓   |  ✓    |   -   |   -   |
| BambuLab A1     |  ✓   |  ✓    |   -   |   -   |

The printer profiles make the printer home the X and Y axis normally and the Z axis at the front of the printbed to avoid collision between the print bed and the, to the tool head attached, pen. Heating is multiple times set to 1°C/33,8°F to prevent routine heating comands from heating up print bed and nozzle.

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

The custom filament profile avoids nozzle and print bed heating and fan cooling during the plot.
For the plot the model should be set to only one layer.

To prevent pen strokes set the Z-Hop int the filament settings under **Settings Overrides > Retraction** between 0.5-1mm and the Z-Hop Type to automatic:
Open Filament Settings:
[image](https://cdn.hackclub.com/019f9ae7-6c37-7d12-b1c5-843d6b0a3e3c/Screenshot%202026-07-24%20235139.png)

Set values as followed:
![image](https://cdn.hackclub.com/019f9ae7-03e8-7768-8caa-ee4e6a7105dd/Unbenannt.png)!
