Introduction
---
This is a accessory for use with Vector LIN tools (or other LIN tools conforming to the Vector pinout) that can be used (with appropriate software configuration, see below) to decode a LIN-CP connection session between an EVSE and EV (and potentially cable assembly).  It requires three connections: Control Pilot, Ground, and any voltage source \~8-45V capable of providing up to 10 mA.  If it is not acceptable to draw vampire power from the EVSE or EV, it can be built to be powered from a 9V battery (see below).

---
Part List
---

| Quantity | Identifier | Description | Example Part Number(s) |
| :------------ | :- |:--------------------------------- | :---------- |
| \~9ft. (\~3m) |    | 18-24AWG (0.25-0.75 mm^2) wire    | |
| 1             |    | 0.1\" (2.5mm) wide zip-tie        | |
| 3             |    | wire clips                        | Keystone 5034/5035 and/or Pomona 3925-3 |
| 1             | U1 | LM317L                            | LM317LBDR2G |
| 1             | C1 | 0.1uF cap X7R pref >=16V 50V pref | CL10B104KB8NNWC |
| 1             | C2 | 0.1-1uF cap X7R or X5R pref >=10V | CL10B104KB8NNWC |
| 1             | R1 | 0603 240r resistor                | RC0603JR-07240RL |
| 1             | R2 | 0603 1k resistor                  | RC0603JR-071KL |
| 1             |    | female DE-9 solder cup connector  | DE09S064TLF or DE09-SD or A-DF 09 LL/Z |
| 1             |    | E size plastic connector shell    | MHCCOV-9-SC-LG or 40-9709H | 
| OPT (1)       |    | 9V battery snap                   | Keystone 232 |

---
PCB
---

Gerber files are provided in `Vector LIN tap v2.zip` and are ready for manufacture.  They can be manufactured in standard 5/5 track/space and should be ordered in standard 1.6 mm thickness.

The PCB layout is in Pulsonix format.  A schematic is not required for such a simple design.  A free [Viewer](https://pulsonix.com/download) is available.

---
Assembly
---

1. Install all surface mount components on PCB (U1, C1-2, R1-2).
2  Insert PCB between the rows of pins on the DE-9 connector such that the numbers on the PCB align with the similarly numbered pins on the connector.
3. Solder all pins on connector to pads on the PCB.
4. Install three wires into the holes on the side of the connector away from the connector.  It is best to install two wires on one side and one on the other, the order does not matter.
5. Install zip-tie around the wires just behind the "T" shaped end of the PCB. 
6. Install the PCB in the shell.  Discard the strain-relief components of the shell (replaced by the zip-tie).
7. Install the wire clips to the loose ends of the wires as appropriate. Ideally they should be color-coded: Red-> PWR, Black->GND, and Orange->CP.

To power the adapter from a 9V battery instead of clipping onto a voltage source in the EVSE or EV, instead of installing the PWR wire (step 4), install the positive lead of the battery snap to the PWR hole and the negative lead in the ground hole, along with the regular ground wire.  Ground must be connected to the CP circuit in either case.  If the EVSE is correctly installed, ground should be connected to earth ground (PE) so any solid connection to earth may be acceptable. Remove the battery from the adapter when not in use.

**_NOTE:_**  Assembly images are of a previous revision requiring rework. 

---
Assembly without PCB
---

Besides convenience, there is no reason that a PCB is required.  Any available ~6.5 voltage source, including an appropriate (properly biased) Zener diode, connected between pins 3 and 9, with pin 4 connected to pin 3, and CP connected to pin 7 will do. See `vector LINCP schematic`. 

---
CANoe Configuration and Use
---
 These instruction are specific to CANoe.  CANalyzer should be similar.
 
 Necessary files and more information are available in [the emulator repo](https://github.com/udv2g/saej3068-emulator).

 "Master Mode" and the master pullup resistor MUST be disabled in the Network Hardware Configuration by first unchecking "Use database Settings", then unchecking the two boxes associated with master mode and the master resistor. ALL interactive generator blocks must then be disabled in Simulation Setup.  These settings WILL randomly be reverted to default if other configuration changes are made.
 