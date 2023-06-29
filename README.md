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
The main PCB contains connection points for both connector types for programming STM32 chips, JTAG and UART. Those can be used for standard pins with 2.54mm distance. Depending on the available connector, you only need one of those two connection point groups. However, I only tested the UART connection. The JTAG connection points have been added to the PCB by following the Mutable Instruments original design.

Besides that, there are two connection points for putting the chip into boot mode, which is needed for loading the bootloader file. Just solder a 1x2 pin with standard 2.54mm distance to connection points labeled "BOOT". For activating the boot mode, place a jumper onto the pins. As soon as the bootloder is uploaded, remove the jumper to put the chip into operation mode, so the main code can be uploaded.

<img width="300" src="https://github.com/TOILmodular/MARBLES/assets/97026614/5aa7d427-7079-4ae4-b69d-208d0d85aa70">

If you want to see more about the chip programming process, you can check out [this YouTube video](xxx).

## Calibration
Calibrating Marbles is more complex than the process for other Mutable Instruments modules. It requires the necessity to adjust and re-compile the source code. That is the reason, why I did not provide the compiled .hex files for this module here, as I did for other Mutable Instruments clones.

Compiling the source code was one of my biggest problems, when trying to build Mutable Instruments clones. Therefore, I provided a [description of the procedure here](https://github.com/TOILmodular/MI_FIRMWARE_COMPILING) to make it as easy as possible for creating .hex files. However, I only used that method with a MAC OS. The alternative is still the process described by Mutable Instruments.

Furthermore for calibrating Marbles, you will need a high-precision multimeter. Mutable Instruments recommends a device capable of 50,000 counts. I used a 40,000 count device.
