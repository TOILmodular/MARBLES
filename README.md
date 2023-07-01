# MARBLES - Random Sampler
A clone of the Mutable Instruments Marbles module.

<img height="500" src="https://github.com/TOILmodular/MARBLES/assets/97026614/6edd362d-fb83-419a-8527-d6d1daaf35c3">
<img height="500" src="https://github.com/TOILmodular/MARBLES/assets/97026614/9f980cb6-fa84-4b9d-8dcd-b115dbb0f78a">

<img height="500" src="https://github.com/TOILmodular/MARBLES/assets/97026614/c3b3ed1f-a07a-4fbe-bb6a-ef1d79c39ea7">
<img height="500" src="https://github.com/TOILmodular/MARBLES/assets/97026614/d2da3a90-14d9-481f-9295-dc352d7ed93e">

## Module Build and PCBs
There are two different versions for the control board, an "original" and a "Thonk" version. Reason is that for my own module, I am using specific potentiometers - 16K4 series from Supertech Electronics - and 3.5mm jack sockets - MJ-355 from Marushin - available at my local electronics shop.

<img width="300" alt="Marbles_CtrlBoardPCB_Orig" src="https://github.com/TOILmodular/MARBLES/assets/97026614/6c3a6cba-d98a-4723-a0a5-a77be741c8ad">

However, since most DIY projects for Eurorack modules out there are using potentiometers from ALPHA and so-called THONKICONN jacks, as they are provided by Thonk in the UK, I also created another control board PCB for the versions "Thonk" with footprints for those components.

<img width="300" alt="Marbles_CtrlBoardPCB_Thonk" src="https://github.com/TOILmodular/MARBLES/assets/97026614/3ab0e54d-33cf-4dd3-9738-83ef58379b9f">

The layout of the main PCB is sligthly different for each version. I needed to move the gate and cv output LED locations, due to the different shape of the jack sockets. Please make sure to use the right control and main board PCBs.

<img width="300" alt="Marbles_MainBoardPCB" src="https://github.com/TOILmodular/MARBLES/assets/97026614/2f680753-b9bb-47d0-bcfd-9a101fb4d7d5">

I created the Gerber files with the online tool EasyEDA and ordered it at JLCPCB.

## Panel Layout
I added the information about hole coordinates for the front panel in the folder PanelLayout, referring to the component layout in the Gerber files. Note that the layout is different for the two PCB versions, due to the LED position differences. Details are explained in the file.

## Additional Information about specific Components
There are several SMD components, which I listed below. 

- STM32F405RGT6 (microcontroller, version 7 is also working fine)
- DAC8164 (DAC, 16-TSSOP package)
- OPA4171 (op amp, 14-SOIC package)
- LD2981ABU33 (voltage regulator, SOT-89-3 package)
- LM4040B10 (voltage regulator, SOT-23-3 package)
- MMBT3904 (transistors, SOT-23-3 package)
- BAT54ST (diode array, SOT-523 package)
- 0.1uF capacitors (1608 package)
- BLM18R (ferrite beads, 1608 package)

Concerning the resistor size, I am usually using small-size resistors, about half the length of the usual size, so they need less space on the PCB. If you want to use my Gerber files, you have to consider that fact. You might still use normal size resistors and put them in a standing position on the boards. Should also work fine.

## Programming
For programming the miroprocessor, you first have to create the bootloader and main .hex files. I did not provide those files here, as the module calibration process requires an adjustment and recompiling of the source code, as described in the calibration section below. For compiling the source code, you can either follow the procedure provided by Mutable Instruments in their [documentation](https://pichenettes.github.io/mutable-instruments-documentation/modules/marbles/open_source/), or you can refer to the method I used in [my other repository](https://github.com/TOILmodular/MI_FIRMWARE_COMPILING). However, I only used that method with a MAC OS. I do not know, if it also works with Windows or Linux.

The main PCB contains connection points for both connector types for programming STM32 chips, JTAG and UART. Those can be used for standard pins with 2.54mm distance. Depending on the available connector, you only need one of those two connection point groups. However, I only tested the UART connection. The JTAG connection points have been added to the PCB by following the Mutable Instruments original design.

Besides that, there are two connection points for putting the chip into boot mode, which is needed for loading the bootloader file. Just solder a 1x2 pin with standard 2.54mm distance to connection points labeled "BOOT". For activating the boot mode, place a jumper onto the pins. As soon as the bootloder is uploaded, remove the jumper to put the chip into operation mode, so the main code can be uploaded.

<img width="300" src="https://github.com/TOILmodular/MARBLES/assets/97026614/5aa7d427-7079-4ae4-b69d-208d0d85aa70">

If you want to see more about the chip programming process, you can check out [this YouTube video](xxx).

## Calibration
Calibrating Marbles is more complex than the process for other Mutable Instruments modules. It requires the necessity to adjust and recompile the source code. That is the reason, why I did not provide the compiled .hex files for this module here, as I did for other Mutable Instruments clones.

As stated above, for the compiling options, either check the [Mutable Instruments documentation](https://pichenettes.github.io/mutable-instruments-documentation/modules/marbles/open_source/) or my repository [MI_FIRMWARE_COMPILING](https://github.com/TOILmodular/MI_FIRMWARE_COMPILING).

Furthermore, for calibrating Marbles you will need a high-precision multimeter. Mutable Instruments recommends a device capable of 50,000 counts. I used a 40,000 count device.

### Measuring CV Outputs
1. Set the voltage range (button J in the MI manual) to +5V (orange LED).
2. Set the T mode (button E) to "coin toss" (green LED).
3. Set the X mode (button N) to "control panel settings for all channels" (green LED).
4. Turn the "Spread" knob fully counter-clockwise.
5. Turn the "Steps" button fully clockwise.
6. Connect the multimeter to CV output X1.
7. Observe the output voltage, while turning the X-side "Bias" knob, until you are as close to 1V as possible (typically a value between 0.9V and 1V).
8. Write down the exact voltage measured. Let's call it 1VX1 (1V for output X1). Ideally, that would be a value with 4 digits.
9. Repeat steps 7 and 8 for 3V. Let's call that measured value 3VX1 (3V for output X1).
10. Repeat steps 7 to 9 for X2 and V3, so you get values 1VX2, 3VX2, 1VX3, 3VX3.
11. For measuring the Y output, keep pressing the X mode button N, while turning the "Spread" knob fully counter-clockwise and the "Steps" knob fully clockwise. Adjust the "Rate" knob to stabilize the CV output value to around 1V, like in step 7. Write down the CV value. Let's call it 1VY.
12. Repeat step 11 with 3V. Let's call that value 3VY.
13. You now should have a list of 8 values for 1VX1, 3VX1, 1VX2, 3VX2, 1VX3. 3VX3, 1VY, 3VY.

### Calculating Offset and Scale
Mutable Instruments provides a script for calculating offset and scale values for each of the 4 output channels, which will have to be added into the source code. If you are not familiar with using such a script (like I was), you can also easily do a manual calculation by using the formulas, given below. You need to calculate a SCALE and OFFSET value for each of the 4 CV outpus (X1, X2, X3, and Y). The variables V1 and V3 are those measured in the previous steps.

***SCALE = -12426 / (V3-V1)***

***OFFSET = 26555 - V1*SCALE***

Example for X2 output:

***SCALE = -12426 / (3VX2 - 1VX2)***

***OFFSET = 26555 - 1VX2*SCALE***

### Adjusting the Source Code
Open the file "settings.cc" of the Marbles source code with a standard text editor and add the following 2 lines for each of the 4 CV outputs at line 179 of the file:

***persistent_data_.calibration_data.dac_offset[< X >] = < OFFSET >f;***

***persistent_data_.calibration_data.dac_scale[< X >] = < SCALE >f;***

Replace ***< X >*** by the following values for each of the CV outputs:

***0*** for Y

***1*** for X1

***2*** for X2

3 for X3

***< OFFSET >*** and ***< SCALE >*** need to be replaced by the calculated values for each CV output.

IMPORTANT!!! Do not forget to put an "***f***" at the end of each of those values!

Example (green part are the added lines):

<img width="300" src="https://github.com/TOILmodular/MARBLES/assets/97026614/64ae85d1-6759-4c9e-8ef5-706cb5f0fb24">

### ADC Calibration
1. Disconnect all cables and long-press the buttons for the Clock Range (button B) and the CV Range (button J).
2. Input 1V (e.g. from a calibrated keyboard) into the Spread CV jack.
3. Press  one of the 2 buttons B or J.
4. Input 3V into the Spread CV jack.
5. Press the button again. 
