# FLEXI-FRAME (Flexible Irradiation Frame System)
<p align="left">
    <img src="https://github.com/user-attachments/assets/2c6fbfe3-6d05-43a5-a77d-c1600c135f57" alt="Description" width="600">
</p>  <br />

# Authors 
- Karolina Klimek
- Pablo Vidal Franco 
# Description of the project 
FLEXI-FRAME (Flexible Irradiation Frame System) is a modular system of movable frames, which can be used to irradiate samples as for example shielding materials, with a particle beam, such as a proton beam. Thanks to its modular structure you can stuck as many frames as you want! It is possible to place a material under tests on the frames and then remotely subsequently put the next layers of the material in the beam. It allows you to check how the transmission changes without accessing the irradiation room many times, which helps to save expensive beam time and reduce unnecessary exposure of personnel to residual radiation. 
# Science and tech used 
Parts needed to make one FLEXI-FRAME: <br />
- RaspberryPi 5 <br />
- Micro Servo 9g SG90 (https://botland.com.pl/serwa-typu-micro/13128-serwo-sg-90-micro-180-5904422350338.html) <br />
- breadboard <br />
- capasitor <br />
- resistor <br />
- two M2 x 10mm screws <br />
- servo horn

To build one FLEXI-FRAME couple of parts need to be 3D printed - .STL files for 3D printing are available in [STL_files](./STL_files/) directory. Constructing one frame requires 5 pieces: frame with a rack, pinion gear, rack holder-top, rack holder-bottom and puzzle servo-frame box. Instructions how to assemble the frame are available [here](./How_to_assemble_a_frame.md). <br />
The concept of using a servo mechanism to convert circular motion into linear motion was inspired by this video: https://www.youtube.com/watch?v=2vAoOYF3m8U. The design was subsequently adapted and modified, including changes to the mechanical layout and the use of a different servo. <br />

# State of the art 
FLEXI-FRAME, in it's first prototype version, allows you to build a modular frame system and remotely place the frames in and out. With a current design you can stack up to 4 frames.
# What next?
Text here... 
# Sources 
- Converting circular motion into linear motion using a servo mechanism ( https://www.youtube.com/watch?v=2vAoOYF3m8U ) 
