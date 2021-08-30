# USB-interfaced-Transistor-Curve-Tracer
This USB interfaced Transistor Curve Tracer is an USB-instrument that collect the data for plotting the static collector curve of an NPN transistor (a family of curves of collector current, I<sub>C</sub>, versus collector-to-emitter voltage, V<sub>CE</sub>, for various values of base current, I<sub>B</sub>.). 

The circuit was made around a PIC18f4550 microcontroller which has built in USB 2.0 capabilities. PIC18f4550It also has 10bit- ADC (Analog to Digital Converter). On the host side (PC/Laptop), a GUI (Graphical User Interface) application has been created (using C#) to operate the device.

## PRINCIPLE OF OPERATION
Three basic functional circuits are used to generate this display: 
1.	A sweep voltage generator for control of the collector voltage (V<sub>CC</sub>). 
2.	A base current (I<sub>B</sub>) source which can be controlled to provide a number of equal increments of base currents with each sweep of the voltage generator.
3.	A timing source to change the base current at the start of each voltage sweep.

The procedure is to set a value of I<sub>B</sub> and hold it fixed while we vary V<sub>CC</sub>. By measuring I<sub>C</sub> and V<sub>CE</sub>, we get the data for graphing I<sub>C</sub> versus V<sub>CE</sub>. Since we know the V<sub>CC</sub>, V<sub>BB</sub>, R<sub>C</sub>, R<sub>B</sub> and we get the value of V<sub>CE</sub> from the device, we can calculate the I<sub>B</sub> and I<sub>C</sub> as follows:
#### I<sub>B</sub>=  (V<sub>BB</sub>-0.7)/R<sub>B</sub>   and   I<sub>C</sub>=  (V<sub>CC</sub>-V<sub>CE</sub>)/R<sub>C</sub>

![Alt text](/Figures/Fig1.png?raw=true "Curve")
###### Figure 1: I<sub>C</sub>-V<sub>CE</sub> Curve of an NPN transistor


![Alt text](/Figures/Fig2.png?raw=true "Schematic Diagram")
###### Figure 2: Schematic Diagram

## MAJOR COMPONENTS
### 1. IC PIC18F4550
![Alt text](/Figures/Fig3_pic18f4550.png?raw=true "PIC18F4550")
###### Figure 3: Micro-Controller PIC18F4550
##### Universal Serial Bus Features:
•	USB V2.0 Compliant
•	Low Speed (1.5 Mb/s) and Full Speed (12 Mb/s)
•	Supports Control, Interrupt, Isochronous and Bulk Transfers
•	Supports up to 32 Endpoints (16 bidirectional)
•	1 Kbyte Dual Access RAM for USB
•	On-Chip USB Transceiver with On-Chip Voltage Regulator
##### Peripheral Highlights:
•	10-Bit, Up to 13-Channel Analog-to-Digital Converter (A/D) module with Programmable Acquisition Time
##### Special Microcontroller Features:
•	C Compiler Optimized Architecture with Optional Extended Instruction Set
•	Wide Operating Voltage Range (2.0V to 5.5V)

### 2. IC DAC0800: Digital to Analog Converter
![Alt text](/Figures/Fig4_dac0800.png?raw=true "DAC0800")
###### Figure 4: IC DAC0800: Digital to Analog Converter
The DAC0800 series are monolithic 8-bit high-speed current-output digital-to-analog converters.
##### DAC0800 Features:
•	Fast settling output current: 100 ns
•	Full scale error: ±1 LSB
•	Nonlinearity over temperature: ±0.1%
•	High output compliance: −10V to +18V
•	Complementary current outputs
•	Interface directly with TTL, CMOS, PMOS and others
•	Wide power supply range: ±4.5V to ±18V
•	Low power consumption: 33 mW at ±5V

### REQUIRED SOFTWARES
Windows' built-in HID (human interface device) driver was used to communicate with the device. There's no need for a custom driver. Any device that can function within the limits of the HID specification (i.e., control and interrupt transfers only) may be able to be designed as an HID. C# was used to develop the host side software (any programming language that supports calling the HID-API functions is okay).
#### For host side software development:
•	Microsoft Visual C# 2008 Express Edition

#### For Firmware development:
•	MPLAB IDE V8.46
•	The Microchip PIC18F Microchip Application Libraries  V2.6a
•	HI-TECH C Compiler for PIC18MCUs Version 9.80 

#### For simulation:
•	Proteus 7 Professional

*All these softwares were freely available from their respective websites.

## THE ALGORITHM
The procedure is to set a value of I<sub>B</sub> and hold it fixed while we vary V<sub>CC</sub>. By measuring I<sub>C</sub> and V<sub>CE</sub>, we get the data for graphing I<sub>C</sub> versus V<sub>CE</sub>. 
_Figure 2_ is shown here again to juxtapose the algorithm with the schematic diagram.
![Alt text](/Figures/Fig2.png?raw=true "Schematic Diagram")

The programs step can be summarized as follows:

**Step 1:** Enumerate the device with the host PC.

**Step 2:** Send from PC to device - the digital equivalent of V<sub>CC</sub> and of V<sub>BB</sub> values

**Step 3:** The device receives the data and set port B and port D accordingly

**Step 4:** Wait for the DAC conversion of the port B (V<sub>CC</sub>) and of port D(V<sub>BB</sub>)Value

**Step 5:** Do the Analog to Digital conversion of the V<sub>CE</sub> and send the value back to host PC

**Step 6:** The host PC writes the data in a file.

**Step 7:** Repeat step-2 to step-6 as many times as needed with different values to produce the curve.


Since we know the V<sub>CC</sub> ,V<sub>BB</sub>, R<sub>C</sub> and R<sub>B</sub> ; and we get the value of V<sub>CE</sub> from the device, we can calculate the I<sub>B</sub> and I<sub>C</sub> as follows:

I<sub>B</sub>= (V<sub>BB</sub> -0.7)/R<sub>B</sub>

I<sub>C</sub>=(V<sub>CC</sub>-V<sub>CE</sub>)/R<sub>C</sub>

Then using the file generated in **step 6**, we plot the I<sub>C</sub>, versus V<sub>CE</sub>, for various values of base current, I<sub>B</sub>.
### Simulation using proteus
Simulator: ISIS Proteus. The circuit looks like this:

![Alt text](/Figures/Fig5_simulation_proteus.jpg?raw=true "Simulation")
###### Figure 5: Simulation in proteus

The following curve was generated from the simulation (Transistor: 2N3904, R<sub>B</sub>=100K ohm, R<sub>C</sub>=1k ohm, I<sub>B</sub>=17.77uA):
The data that produced the curve is in the file 'SimulatedData.txt'.

![Alt text](/Figures/Fig6_curve_simulated.png?raw=true "Curve")
###### Figure 6: Simulated  I<sub>C</sub> versus V<sub>CE</sub> curve


## Code Explanation
There are two separate programs, one in the host PC/Laptop and the other in the microcontroller of the curve tracer. 
### Host Side
The host side program uses a series of API calls to locate a HID-class device by its Vendor ID and Product ID. It returns _True_ if the device is detected, _False_ if not detected. 

If the device is detected, the device is registered to the OS for receiving notifications regarding the removal or attachment to the USB-port. Data is trnsferred to and from the device using reports. The program gets _handles_ to use for requesting _Input reports_ from the curve tracer device and generating _Output reports_ to .

If the device wasn't detected, the information is displayed in the form's list box.

When the EXECUTE button is pressed, the function ReadAndWriteToDevice(i, j) is called with various values of  i (PORT B=V<sub>BB</sub>) and j(PORT D=V<sub>CC</sub>) in a loop.

**ReadAndWriteToDevice(i, j)** function tries to write the values into Feature Report Buffer. If it succeeds, it then reads the response (VCE) sent by the device from the Feature Report Buffer. Both the written and read values are then stored in a text file. This text file is then used to draw the curves.





