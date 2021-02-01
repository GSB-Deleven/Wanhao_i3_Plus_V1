# Calibrate EEPROM

https://www.youtube.com/watch?v=25r-PTVJDjQ&t=9s

M503 response:
```
Recv: echo:Steps per unit:
Recv: echo:  M92 X80.00 Y80.00 Z397.00 E100.00
Recv: echo:Maximum feedrates (mm/s):
Recv: echo:  M203 X450.00 Y450.00 Z5.00 E25.00
Recv: echo:Maximum Acceleration (mm/s2):
Recv: echo:  M201 X3000 Y3000 Z100 E3000
Recv: echo:Acceleration: S=acceleration, T=retract acceleration
Recv: echo:  M204 S1000.00 T800.00
Recv: echo:Advanced variables: S=Min feedrate (mm/s), T=Min travel feedrate (mm/s), B=minimum segment time (ms), X=maximum XY jerk (mm/s),  Z=maximum Z jerk (mm/s),  E=maximum E jerk (mm/s)
Recv: echo:  M205 S0.00 T0.00 B20000 X20.00 Z0.40 E1.00
Recv: echo:Home offset (mm):
Recv: echo:  M206 X0.00 Y0.00 Z0.00
Recv: echo:PID settings:
Recv: echo:   M301 P32.54 I2.29 D115.70
Recv: ok

```

## Measured Calibration Cube X Y Z  
* X = 19.80  
* Y = 19.80  
* Z = 20.30
---
* Calculation: (Target (20) / Result) x Current Value
* **X = (20/19.80)x79.22 = 80.02**
* **Y = (20/19.80)x79.41 = 80.21**
* **Z = (20/20.30)x403.57 = 397.61**
---
```
M92 X80.02 Y80.21 Z397.61
```


Extruder:  
* 120mm Target
	* 1 = 120 - 16.15 = 103.85
	* 2 = 
	* 3 =
	* 4 =
	* 5 =
	* Durchschnitt =
*  Calculation: (Target (100) / Result) x Current Value
```
M92 E96.29
```
Check if it got accepted with
```
M503
````
Check if it does it correctly by ectruding another 120mm and 20mm should be left.

If so safe the value with
```
M500
````
