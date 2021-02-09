As `M600` or `M601` doesnt work with the Wanhao Duplicator i3 Plus V1 i figuered out this workaround

If you send the `@pause` command in a GCODE and run it in Octoprint, it will trigger the Octoprint pause script.
So it is super easy in Prusa slicer.

* Slice the model
* go to the traget layer 
* rightclick on the layer selector
* add custom gcode
![](https://github.com/GSB-Deleven/Wanhao_i3_Plus_V1/blob/main/images/PrusaSlicer_Pause.jpg?raw=true)
* type in `@pause`
* it will pause now on this layer

---

Same thing if you want to do custom Temperature or so at a layer hight (typical for Temp towers)  
  
There you just insert `M104 S225` at the desired layer
* `M104` is the change Temperature command
* `S225` is the Temperature it should change
![](https://raw.githubusercontent.com/GSB-Deleven/Wanhao_i3_Plus_V1/main/images/Temp%20Tower_Gcode.jpg)
