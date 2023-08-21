# MARBLES - Random Sampler
A clone of the Mutable Instruments Marbles module.

<img height="500" src="https://github.com/TOILmodular/MARBLES/assets/97026614/82fb32af-2d25-4a50-a6ca-b1fbbde70a2b">
<img height="500" src="https://github.com/TOILmodular/MARBLES/assets/97026614/7c43b14d-eb07-49ce-a214-7a61f9110750">

<img height="500" src="https://github.com/TOILmodular/MARBLES/assets/97026614/68dcdcdb-f269-4342-8198-e0ba8f067db5">
<img height="500" src="https://github.com/TOILmodular/MARBLES/assets/97026614/246b8f7c-51aa-43aa-b566-f3ff96945356">

## Module Build and PCBs
There are two different versions for the control board, an "original" and a "Thonk" version. Reason is that for my own module, I am using specific potentiometers - 16K4 series from Supertech Electronics - and 3.5mm jack sockets - MJ-355 from Marushin - available at my local electronics shop.

<img width="300" alt="Marbles_CtrlBoardPCB_Orig" src="https://github.com/TOILmodular/MARBLES/assets/97026614/e1b48a03-b0a1-45ba-ae6c-539c568768b0">

However, since most DIY projects for Eurorack modules out there are using potentiometers from ALPHA and so-called THONKICONN jacks, as they are provided by Thonk in the UK, I also created another control board PCB for the version "Thonk" with footprints for those components.

<img width="300" alt="Marbles_CtrlBoardPCB_Thonk" src="https://github.com/TOILmodular/MARBLES/assets/97026614/fff32ecc-1089-4aa4-b18a-9a4ef8cedd3e">

The layout of the main PCB is sligthly different for each version. I needed to move the gate and CV output LED locations, due to the different shape of the jack sockets. Please make sure to use the right control and main board PCBs.

<img width="300" alt="Marbles_MainBoardPCB" src="https://github.com/TOILmodular/MARBLES/assets/97026614/03fac540-ce6f-43c9-8b48-698aff692b23">

I created the Gerber files with the online tool EasyEDA and ordered it at JLCPCB.

## Panel Layout
I added the information about hole coordinates for the front panel in the folder PanelLayout, referring to the component layout in the Gerber files. Note that the layout is different for the two PCB versions, due to the LED position differences. Details are explained in the layout description.

In addition, there are two versions of Gerber files for the panel, following the HP standard. My own modules do not follow that width standard, as I am only using sliding nuts in my racks. The mentioned difference between the two control PCB versions is also reflected in the two panel versions. Choose the one, depending on your control PCB version.

You can use the panel Gerber files to have the panel built out of PCB material.

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

## Firmware and Programming
For programming the miroprocessor, I added the bootloader and main .hex files in the folder Firmware. The module calibration process requires an adjustment and recompiling of the main source code, as described in the calibration section below. Please also check the ReadMe file in the folder Firmware.

For compiling the source code, you can either follow the procedure provided by Mutable Instruments in their [documentation](https://pichenettes.github.io/mutable-instruments-documentation/modules/marbles/open_source/), or you can refer to the method I used in [my other repository](https://github.com/TOILmodular/MI_FIRMWARE_COMPILING). However, I only used that method with a MAC OS. I do not know, if it also works with Windows or Linux.

The main PCB contains connection points for both connector types for programming STM32 chips, JTAG and UART. Those can be used for standard pins with 2.54mm distance. Depending on the available connector, you only need one of those two connection point groups. However, I only tested the UART connection. The JTAG connection points have been added to the PCB by following the Mutable Instruments original design.

Besides that, there are two connection points for putting the chip into boot mode, which is needed for loading the bootloader file. Just solder a 1x2 pin with standard 2.54mm distance to connection points labeled "BOOT". For activating the boot mode, place a jumper onto the pins. As soon as the bootloder is uploaded, remove the jumper to put the chip into operation mode, so the main code can be uploaded.

<img width="300" src="https://github.com/TOILmodular/MARBLES/assets/97026614/ab59a136-bf83-43a7-a583-e7ac8bfa90cb">

If you want to see more about the chip programming process, you can check out [this YouTube video](https://youtu.be/9D4ZEAn3BBg) for my Plaits DIY clone, as the procedure is the same.

## Calibration
Calibrating Marbles is more complex than the process for other Mutable Instruments modules. It requires to adjust and recompile the source code. The compiled .hex files for this module here are only for getting the module to work, so the actual calibration can be performed.

As stated above, for the compiling options, either check the [Mutable Instruments documentation](https://pichenettes.github.io/mutable-instruments-documentation/modules/marbles/open_source/) or my repository [MI_FIRMWARE_COMPILING](https://github.com/TOILmodular/MI_FIRMWARE_COMPILING).

Furthermore, for calibrating Marbles you will need a high-precision multimeter. Mutable Instruments recommends a device capable of 50,000 counts. I used a 40,000 count device.

The below procedure is also demonstrated in my [YouTube video](https://youtu.be/d1dFJfD5AMo).

### Measuring X1-X3 CV Outputs
1. Set the voltage range (button J in the MI manual) to +5V (orange LED).
2. Set the X mode (button N) to "control panel settings for all channels" (green LED).
3. Turn the "Spread" knob fully counter-clockwise to keep the CV output signals constant.
4. Turn the "Steps" button fully clockwise to set the quantization to octaves.
5. Connect the multimeter to CV output X1.
6. Observe the output voltage, while turning the X-side "Bias" knob, until you are as close to 1V as possible (typically a value between 0.9V and 1V).
7. Write down the exact voltage measured. Let's call it X11V (1V for output X1). Ideally, that would be a value with 4 digits.
8. Repeat steps 7 and 8 for 3V. Let's call that measured value X13V (3V for output X1).
9. Repeat steps 7 to 9 for X2 and V3, so you get values X21V, X23V, X31V, X33V.

### Measuring Y CV Output
1. Keep pressing the X mode button (N), while turning the "Spread" knob fully counter-clockwise.
2. Keep pressing the X mode button (N), while turning the "Steps" knob fully clockwise. 
3. Move the "Bias" knob of the X generator side to set the Y CV output as close to 1V, as possible (typically a value between 0.9V and 1V). Play around with the "Rate" knob to change and then stabilize the Y CV output.
4. Write down the CV value. Let's call it 1VY.
5. Repeat steps 3 and 4 with 3V. Let's call that value 3VY.

You now should have a list of 8 values for X11V, X13V, X21V, X23V, X31V. X33V, Y1V, Y3V.

### Calculating Offset and Scale
Mutable Instruments provided a linkto a Jupyter Notebook script in their [Marbles documentation](https://pichenettes.github.io/mutable-instruments-documentation/modules/marbles/open_source/) for calculating offset and scale values for each of the 4 output channels, which will have to be added into the source code. You will need to logon to a Google account for executing that script. 

Alternatively, you can also do a manual calculation by using the formulas, given below. You need to calculate a ***SCALE*** and ***OFFSET*** value for each of the 4 CV outputs (X1, X2, X3, and Y). The variables ***XY1V*** and ***XY3V*** are those measured in the previous steps. ***XY*** stands for the different CV outputs X1, X2, X3, and Y.

***SCALE_XY = -12426 / (XY3V - XY1V)***

***OFFSET_XY = 26555 - XY1V * SCALE_XY***

Example for X2 output:

***SCALE_X2 = -12426 / (X23V - X21V)***

***OFFSET_X2 = 26555 - X21V * SCALE_X2***

### Adjusting the Source Code
Open the file "settings.cc" of the Marbles source code with a standard text editor and add the following 2 lines for each of the 4 CV outputs at line 179 of the file:

***persistent_data_.calibration_data.dac_offset[< X >] = < OFFSET_XY >f;***

***persistent_data_.calibration_data.dac_scale[< X >] = < SCALE_XY >f;***

Replace ***< X >*** by the following values for each of the CV outputs:

***0*** for Y

***1*** for X1

***2*** for X2

***3*** for X3

***< OFFSET_XY >*** and ***< SCALE_XY >*** need to be replaced by the calculated values for each CV output.

IMPORTANT!!! Do not forget to put an "***f***" at the end of each of those values!

Example (green part are the added lines):

<img width="300" src="https://github.com/TOILmodular/MARBLES/assets/97026614/ead3d160-1677-4581-8778-772849e0ff39">

### ADC Calibration
1. Disconnect all cables and long-press the buttons for the Clock Range (button B) and the CV Range (button J). The Clock Range LED will blink green.
2. Input 1V (e.g. from a calibrated keyboard) into the Rate CV.
3. Press  one of the 2 buttons B or J. The Clock Range LED will blink orange.
4. Input 3v into the Rate CV.
5. Press the button again. The CV Range LED will blink green.
6. Input 1V into the Spread CV.
7. Press the button again. The CV Range LED will blink orange.
8. Input 3V into the Spread CV.
9. Press the button again.
