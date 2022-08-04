# Stanford-Environmental-Chamber
For the fabrication and operation of the Stanford Environmental Chamber
Device Construction and List of Materials 

Standard materials and tools were used for the construction of our optical imaging chamber. Any special or unique tools that were utilized in the operation and construction of our imaging chamber will be detailed below. All systems were constructed outside of an inert atmosphere and transferred into the glovebox via the front window. 

Chamber Set-up 



















Figure 1: Design of the Stanford Optical Imaging Chamber


The chamber is comprised of: 
1)	ThorLabs Compact 12.3MP Scientific Camera (CS126CU)
2)	ThorLabs MVL12M1 C-mount Lens
3)	ThorLabs Black Hardboard Enclosure (XE25C9D)
4)	Two Linear White Backlights from Advanced Illumination (BL 313)
5)	Advanced Illumination Three-port Controller (DCS-103E) and standard ethernet cable
6)	24V, 4.5A Computer Power Supply and AC wall outlet power cable 
7)	XRite Color Checker Passport Photo 2
8)	ThermoFisher Aluminum Metal SuperNuova+ Hotplate 
9)	3D Printed Mounts for holding camera/lens, lights, and electronics in place 
10)	Large black acrylic board for mounting the enclosure 
11)	Optional aluminum sample alignment mask with heat-proof black paint 


Full Build and Operation Guide of the Enclosure 

1)	Constructing the Frame 
•	The ThorLabs black hardboard enclosure should be constructed in accords with original manufacturer instructions. 
•	The black acrylic can be drilled in the four corners and affixed to the bottom of the hardboard corners via M6 screws with washers. 
•	Three small holes can be drilled in the side of the hardboard to accommodate cord feedthroughs for the two lights and hotplate 

2)	Mounting the Hotplate and Color Checker 
•	The ThermoFisher hotplate is inserted with the doors of the hardboard enclosure off for ease of access so that the center of the aluminum portion of the hotplate is directly in the center of the box. 
•	Corner mounts for the four corners of the hotplate can optionally be added to mitigate optical drift by ensuring the hotplate stays fixed in place (Eight, M6 or M8 screws and nuts work well for this with holes drilled at a 45º diagonal over the hotplate corner to keep the hotplate from moving). This step, while optional, allows for the box to be moved into the glovebox with ease and with retaining alignment. 
•	Using the rod stand holder manufactured on the hotplate, a 3D printed mount (CC_Mount.step) for the color checker can be printed to hold the Color Checker in view of the camera during all tests though this component is optional if the system is run similarly to MIT’s work. 
•	A laser cutter or drill hole borer should be used to cut a round, 7.48 in hole into the top of the hardboard enclosure centered above the hotplate for mounting the camera. Note: this hole size and camera mount distance can be adjusted and optimized for particular camera architectures and hotplate sizes 

3)	Mounting the Illumination Set-up
•	Behind the box, mount the 24V/4.5A DC power supply for the lamps along with the DCS-103E controller 
•	Run the two backlight cords into the interior of the box
•	Mount the two lights at either end of the box with mounts that are 45º relative to the box top facing the face of the hotplate. These mounts can be printed using “Light Mount Brackets.step” out of a high temperature compatible 3D printable polymer 
•	Install the DCS Advanced Illumination test software to ensure proper operation of the two lights in unison.

4)	Camera Mounting 
•	Over the drilled opening on the top of the hardboard enclosure, two 3D printed components will be mounted which are the optical extender and the lens mount (“Lens Mount Extender.step” and “Lens Mount Camera Holder.step”). The extender gives you sufficient field of view while the mount holds the camera and lens in the proper position. (see Figure 1 above to the arrow labeled “3D-printed Camera Mount” 
•	Due to ease of printing, the lens mount and extender are printed separately and then glued together with standard super glue
•	Use the camera’s C-mount and screw on the lens in accord with manufacturer’s instructions 
•	Use M6 screws, nuts, and washers to mount the full 3D printed assembly to the top of the hardboard aligned over the laser cut hole. 

5)	Software Installations
The following software packages are needed to operate the Stanford Optical System
•	LabView VI 
o	ThorCam’s LabView integration subVIs (from ThorLab’s website) 
o	Dll library of ThorCam Scientific Camera interfaces (from ThorLab’s website) 
o	ThorCam LabView Controls folder (from ThorLab’s website) 
•	DSC-103E Graphical User Interface Software 
•	Python to run Main.py and Colorchecker.py provided from MIT
o	Numpy 
o	Pandas
o	Matplot.lib
o	RGB extractor
o	PIL
o	Colormap
Additional recommended software packages: 
•	GIMP or another facile RGB image analyzer/viewing tool 
•	ThorCam Software for Scientific Cameras (used for tool alignment) 

6)	Install Enclosure in the Glovebox 
Ensuring the proper feedthroughs are available (1 USB, 1 Ethernet, and 2 power outlets), install the full unit into an N2 or other inert atmosphere glovebox. 

7)	Initialize a Run 
•	Preheat hotplate to desired temperature 
•	Place devices front electrode down onto the hotplate in the desired configuration or into the sample mask 
•	Open a python compiler with main.py and colorchecker.py 
•	Open LabView VI for either continuous illumination measurements or with flash illumination measurements 
o	Number 1: Repetitive Imaging Loop will run the system with the light flashing only during imaging 
o	Number 2: Illuminated Repetitive Imaging Loop will run the system with continuous illumination
•	Open the VI (ensure that all necessary supporting packages are in appropriate subfolders and can be located by LabView, any that cannot be found have been moved or deleted and must be replaced in their original location)
•	When the VI is open, hover the cursor over the File Path textbox until it changes to the text pointer, then type in the desired path for images to be saved to. Alternatively, click on the folder icon below the File Path textbox and browse for and select the desired path.
•	There are a number of parameters with default values. These values can be left alone or changed as desired by hovering the cursor over the parameter box until it changes to the text pointer and clicking. Then your parameter can be entered. 
•	Recommended preset values include:
o	Gain = 1
o	Exposure Time = 30 sec
o	Light Warm-up Time = 5 sec
o	Light Brightness = 75 mA
o	Good Starting Points for RGB Gains: R = 3, G =1, B =3.1 
•	The same action is followed to enter values for parameters without default values. These parameters must all be filled for the VI to operate properly.
•	Important to note that the Light Warmup Time parameter must be smaller than the Photo Interval parameter.
•	The Exposure and Gain parameters effect the camera and image’s brightness, while the Light Level (left and right) parameters effect the lights themselves and determine the illumination inside the imaging area. These will likely be different for the illuminated vs the dark aging tests, and they will likely have different default parameters as well. 
•	Once parameters are set, make sure that LabView is not in debugging mode by checking that the lightbulb in the top left of the window is grey (not yellow). Then, if substrates are in place and the hotplate is on, click the play button in the top left to start the program to start the test for the desired time. 

8)	Analyzing Photo Data
•	Photograph data will be stored in the folder outlined in LabView
•	Using colorchecker.py, adjust the coordinates of the color panels for normalization 
•	Ensure over-saturation is not occurring using GIMP or similar software to ensure the white square is not above RGB = 255,255,255
•	Using main.py, adjust the analysis area to the module architecture of choice and analyze the RGB values 
•	Allow the software to run and output the normalized RGB color values for the devices being analyzed  
