

# FLEXI-FRAME (Flexible Irradiation Frame System)
<p align="center">
    <img src="https://github.com/user-attachments/assets/2c6fbfe3-6d05-43a5-a77d-c1600c135f57" alt="Description" width="600">
</p>

# Authors 
- Karolina Klimek
- Pablo Vidal Franco

# Description of the project 
FLEXI-FRAME (Flexible Irradiation Frame System) is a modular system of movable frames, which can be used to irradiate samples (e.g. shielding materials), with a particle beam, such as a proton beam. Thanks to its modular structure you can piece together as many frames as you want! It is possible to place a material under tests on the frames and then remotely put the next layers of the material in the trajectory of the beam, in a subsequent manner. It allows you to check how the transmission changes without accessing the irradiation room many times, which helps to save expensive beam time and reduce unnecessary exposure of personnel to residual radiation. 

# Science and tech used 

## List of materials
Parts needed to make one FLEXI-FRAME: <br />
- RaspberryPi 5 <br />
- Micro Servo 9g SG90 (https://botland.com.pl/serwa-typu-micro/13128-serwo-sg-90-micro-180-5904422350338.html) <br />
- Breadboard <br />
- 220 $\mu F$ capacitor <br />
- 470 $\Omega$ resistor <br />
- LED (2.5-3.7 V)
- Two M2 x 10mm screws <br />
- Screw terminal
- USB-C power adapter (5 V 3 A)
- Servo horn

## Servo specifications
- Logic level compatibility 3.3 V logic
- Operating voltage 4.8 V - 6.0 V
- Average running current: 250 mA
- Stall current: 360 mA

## Power source for the servos
A standard phone charger USB-C power adapter (Dux Ducis) with an output of 5 V 3 A can be repurposed by cutting open the cable and separating VBUS and GND lines into a screw terminal, connected to a prototype breadboard rail power and GND rails.

The total available power is:

$$
P_{total} = 5\ \text{V} \cdot 3\ \text{A} = 15\ \text{W}
$$

Power consumption per servo is:

$$
P_{servo} = 5\ \text{V} \cdot 0.25\ \text{A} = 1.25\ \text{W}
$$

Maximum theoretical number of servos that this setup can handle:

$$
n_{servos} = \frac{P_{total}}{P_{servo}} = \frac{15\ \text{W}}{1.25\ \text{W}} = 12
$$

Therefore, assuming current draw remains consistent and below the 3 A limit, the USB-C adapter can power 4 servos stably.

## Capacitor for stability
To buffer transient load steps on the 5 V servo rail before the power supply fully responds, a 220 µF electrolytic low-ESR capacitor is placed across +5 V and GND near the servo power split. Assuming $\Delta I$ is the current stall of a single servo (an upper bound of 360 mA), and assuming that only one servo will be operated at a given timestep, we have the following values:

$$
\Delta I = 0.36\ \mathrm{A},\quad
\Delta t = 2\ \mathrm{ms},\quad
C = 220\ \mu \text{F},\quad
V = 5\ \mathrm{V}
$$

The extra charge drawn by the step:

$$
\Delta Q = \Delta I\ \Delta t = 360\ \mathrm{mA} \cdot 2 \mathrm{ms} = 720 \ \mu \text{C}
$$


Now we can compare the capacitor stored charge ($Q_{total}$) against two scenarios:
- 1 servo demanding extra charge in a 2 ms step ($\Delta Q_{single} = 720 \ \mu \text{C}$)
- A worst-case scenario where 4 servos demand extra charge in a 2 ms step ($\Delta Q_{multiple} = 720 \ \mu \text{C} \cdot 4 = 2880\ \mu \text{C}$)

We compare the total charge stored by the 220 $\mu F$ capacitor against the two scenarios:

$$ Q_{total} = CV = 220\ \mu \text{F} \cdot 5\ \mathrm{V} = 1100\ \mu \text{C}, \quad \Delta Q_{single} \le Q_{total}, \quad \Delta Q_{multiple} \ge Q_{total}
$$

We can assume 10% of our 5 V budget to power the servos and compute how long can the USB-C power adapter fail in both scenarios:

$$
\Delta t_{\max}\ = \frac{C \cdot \Delta V_{\text{target}}\ }{\Delta I} = \frac{220\ \mu \text{F} \cdot 0.5\ \text{V}}{360\ \text{mA}} \approx 0.306 \mathrm{ms}
$$

$$
\Delta t_{\max}\ = \frac{C \cdot \Delta V_{\text{target}}\ }{\Delta I} = \frac{220\ \mu \text{F} \cdot 0.5\ \text{V}}{1440\ \text{mA}} \approx 0.076 \mathrm{ms}
$$

We can conclude that the current capacitor system could handle a single servo stalling during transient current supply ($\le0.306\ \text{ms}$) while limiting voltage droop to 0.5 V (10% of the 5 V needed for servo operation), but could not handle 4 servos stalling at the same time unless the USB-C power adapter recovers in less than 0.076 ms. 

## Wiring diagram
<p align="center">
<img width="875" height="952" alt="pic_garage" src="https://github.com/user-attachments/assets/82f45699-2919-4b2f-865a-f0d5352d8581" />
</p>

## Assembly instructions
To build one FLEXI-FRAME couple of parts need to be 3D printed - .STL files for 3D printing are available in [STL_files](./STL_files/) directory. Constructing one frame requires 5 pieces: frame with a rack, pinion gear, rack holder-top, rack holder-bottom and puzzle servo-frame box. Instructions how to assemble the frame are available [here](./How_to_assemble_a_frame.md). <br />
The concept of using a servo mechanism to convert circular motion into linear motion was inspired by this video: https://www.youtube.com/watch?v=2vAoOYF3m8U. The design was subsequently adapted and modified, including changes to the mechanical layout and the use of a different servo. <br />

# State of the art 
FLEXI-FRAME, in its first prototype version, allows you to build a modular frame system and remotely control the frames in and out of the beam's trajectory. With the current design you can stack up to 4 frames, using servos sequentially.

# What next?
- Creating a rail structure to ensure stable linear motion when moving the frame in or out.
- Wiring frame-motion sensors and building a UI interface that lets the user know what is the current state of each frame.
- Improve the capacitor buffer system to support up to $n_{servos}$ in a worst-case scenario, to allow safer multiple non-sequential servo operation.

# Sources 
- Converting circular motion into linear motion using a servo mechanism (https://www.youtube.com/watch?v=2vAoOYF3m8U)
- Servo specs (https://protosupplies.com/product/servo-motor-micro-sg90/)
