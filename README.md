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

![Alt text](/Fig1.png?raw=true "Curve")
###### Figure 1: I<sub>C</sub>-V<sub>CE</sub> Curve of an NPN transistor


![Alt text](/Fig2.png?raw=true "Schematic Diagram")
###### Figure 2: Schematic Diagram

## MAJOR COMPONENTS
### 1. IC PIC18F4550
![Alt text](/Fig3_pic18f4550.png?raw=true "PIC18F4550")
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
The DAC0800 series are monolithic 8-bit high-speed current-output digital-to-analog converters.
![Alt text](/Fig4_dac0800.png?raw=true "DAC0800")
###### Figure 4: IC DAC0800: Digital to Analog Converter
##### DAC0800 Features:
•	Fast settling output current: 100 ns
•	Full scale error: ±1 LSB
•	Nonlinearity over temperature: ±0.1%
•	High output compliance: −10V to +18V
•	Complementary current outputs
•	Interface directly with TTL, CMOS, PMOS and others
•	Wide power supply range: ±4.5V to ±18V
•	Low power consumption: 33 mW at ±5V
•	Low cost
