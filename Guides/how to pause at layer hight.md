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
