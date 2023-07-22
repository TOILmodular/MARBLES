# CAUTION
The .hex files for the bootloader and the main code provided here are compiled from the Mutable Instruments original source code without any change. By using those files, the DAC will not be calibrated, and the quantizer will be out of tune.

Use the files for the initial programming of the microcontroller, so the module can be calibrated. The calibration procedure for the module requires the adjustment of the file *settings.cc*, and the main code (*marbles.hex*) needs to be recompiled.

The procedure is described in the section *Calibration* of the main ReadMe file.
