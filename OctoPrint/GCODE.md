After print job is cancelled
```gcode
; disable motors
M84

;disable all heaters
{% snippet 'disable_hotends' %}
{% snippet 'disable_bed' %}
;disable fan
M106 S0
```


After print job is paused

```gcode
{% if pause_position.x is not none %}
; relative XYZE
G91
M83

; retract filament, move Z slightly upwards
G1 Z+5 E-5 F4500

; absolute XYZE
M82
G90

; move to a safe rest position, adjust as necessary
G1 X0 Y0
{% endif %}
```

Before print job is resumed
```gcode
{% if pause_position.x is not none %}
; relative extruder
M83

; prime nozzle
G1 E-5 F4500
G1 E5 F4500
G1 E5 F4500

; absolute E
M82

; absolute XYZ
G90

; reset E
G92 E{{ pause_position.e }}

; move back to pause position XYZ
G1 X{{ pause_position.x }} Y{{ pause_position.y }} Z{{ pause_position.z }} F4500

; reset to feed rate before pause if available
{% if pause_position.f is not none %}G1 F{{ pause_position.f }}{% endif %}
{% endif %}
```
-------

# Careful this is my standard Cura Code, I think it acts up on OctoPrint

Start GCODE:
```gcode
G21 ;metric values
G90 ;absolute positioning
M82 ;set extruder to absolute mode
M107 ;start with the fan off
G92 E0; set extruder to 0;
G28 X0 Y0 ; move X/Y to min endstops
G28 Z0 ; move Z to min endstops
G1 Y-3.0 F500.0 ; move out of print volume
G1 X60.0 E9 F500.0 ; start purge line
G1 X100.0 E12.5 F500.0 ; finish purge line
```

End GCODE:
```gcode
M104 S0 ;extruder heater off 
M140 S0 ;bed heater off 
G91 ;relative positioning 
G1 E-1 F300 ;retract the filament 1mm 
G1 Z+0.5 E-3 X-20 Y-20 F6000 ;move Z up and retract filament 3mm 
M106 S255 ;fan at 100% to cool nozzle 
G90 ;absolute positioning 
G28 X0 Y0 ;home X and Y 
G1 Y190 ;move bed forward 
M84 ;steppers off 
G4 P120000 ;wait 2 minutes (120 seconds) 
M106 S0 ;fan off

```
