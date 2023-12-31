## Panel Layout for PCB

The panel dimensions provided in the section "Original Design" below are based on my own module build, since I am not following the standard HP (1HP eq. 5.08mm) size. An alternative by building an HP-standard size panel can be found in the section "HP Standard Design" further below.

### Original Design
Coordinates given in the table fit to the layout of components given in the PCBc in folder GerberFiles.
The layout is slightly different for both versions due to different positions of the output LEDs. Details are given in the coordinates table below.

Panel size: 90mm x 128.5mm

The numbers in the table are refering to the numbers in the picture below.
Coordinates origin is the lower left corner of the panel.


| No. | X-coord. [mm] | Y-coord. [mm] | Comment |
| --- | --- | --- | --- |
| 1 | 6 | 106 | T Freeze Button |
| 2 | 12 | 106 | T Freeze LED |
| 3 | 45 | 106 | Deja-Vu Pot |
| 4 | 78 | 106 | X Freeze LED |
| 5 | 84 | 106 | X Freeze Button |
| 6 | 6 | 94 | T Mode LED |
| 7 | 6 | 88 | T Mode Button |
| 8 | 21 | 95 | Rate Pot |
| 9 | 69 | 95 | Spread Pot |
| 10 | 84| 94 | X Mode LED |
| 11 | 84 | 88 | X Mode Button |
| 12 | 30 | 78 | Clock Range LED |
| 13 | 45 | 80 | Length Pot |
| 14 | 60 | 78 | CV Range LED |
| 15 | 11 | 72 | T Bias Pot |
| 16 | 30 | 72 | Clock Range Button |
| 17 | 60 | 72 | CV Range Button |
| 18 | 79 | 72 | X Bias Pot |
| 19 | 45 | 62 | Ext Sample Mode Button |
| 20 | 27 | 55 | Jitter Pot |
| 21 | 45 | 56 | Ext Sample LED |
| 22 | 63 | 55 | Steps Pot |
| 23 | 9 | 49 | T Bias CV Jack |
| 24 | 81 | 49 | X Bias CV Jack |
| 25 | 9 | 34 | T Clock Jack |
| 26 | 21 | 34 | Rate CV Jack |
| 27 | 33 | 34 | Jitter CV Jack |
| 28 | 45 | 34 | Deja Vu CV Jack |
| 29 | 57 | 34 | Steps CV Jack |
| 30 | 69 | 34 | Spread CV Jack |
| 31 | 81 | 34 | X Clock Jack |
| 32 | 9 | see footnote *) | T1 Output LED |
| 33 | 21 | see footnote *) | T2 Output LED |
| 34 | 33 | see footnote *) | T3 Output LED |
| 35 | 45 | see footnote *) | Y Output LED |
| 36 | 57 | see footnote *) | X1 Output LED |
| 37 | 69 | see footnote *) | X2 Output LED |
| 38 | 81 | see footnote *) | X3 Output LED |
| 39 | 9 | 15 | T1 Output Jack |
| 40 | 21 | 15 | T2 Output Jack |
| 41 | 33 | 15 | T3 Output Jack |
| 42 | 45 | 15 | Y Output Jack |
| 43 | 57 | 15 | X1 Output Jack |
| 44 | 69 | 15 | X2 Output Jack |
| 45 | 81 | 15 | X3 Output Jack |

*) Y-coordinate = 21 for "original" design. Y-coordinate = 23 for "Thonk" design.

<img height="1200" src="https://github.com/TOILmodular/MARBLES/assets/97026614/c77d0bc2-0eea-48b1-85d0-ef07512f84f9">

### HP Standard Design
For building the panel with a size following the HP standard, you can use the panel Gerber files provided in the folder "GerberFiles".

There are two versions ("Orig" and "Thonk"), since the positions of some of the LEDs are slightly different, due to the jack size difference for the two versions.

I ordered my own panel via such gerber file built out of PCB material.

Here are a few parameters of the panel.
| Parameter | Value |
| --- | --- |
| Width | 18HP |
| Pot hole diameter | 8mm |
| Jack hole diameter | 6.1mm |
| Tact switch hole diameter | 5.1 mm |
| LED hole diameter for X and T Deja-vu, external sampling, T, Y and X outputs | 3.1mm|
| LED hole diameter for X and T modes, clock range, CV range | 5.1mm|
| Mounting hole diameter | 3.2mm|
