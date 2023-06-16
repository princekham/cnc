# cnc
Notes on my CNC plasma table

Limit Switch one to IN1 and the other to ground

Stepper motor driver setup
- Ampere requirement according to Nema 23 specs is 2.8 A, so I will set it to 3.31A which is off, on, off for switch 1,2,3
- For microstepping 3200 is chosen which is on on off on for switch 5, 6, 7, 8
- switch 4 is off for Half current



![image](https://github.com/princekham/cnc/assets/16104631/0bff4730-1928-4a17-831b-914c8bd0b21c)

Testing with Arduino and DM542 (Source : https://mytectutor.com/tb6600-stepper-motor-driver-with-arduino/)


![image](https://github.com/princekham/cnc/assets/16104631/8be45634-7d00-4f53-a1f1-6df77faaf471)


const int stepPin = 5; 
const int dirPin = 2; 
const int enPin = 8;

void setup() {
  pinMode(stepPin,OUTPUT); 
  pinMode(dirPin,OUTPUT);
  pinMode(enPin,OUTPUT);
  digitalWrite(enPin,LOW);
  
}

void loop() {
  digitalWrite(dirPin,HIGH); // Enables the motor to move in a particular direction
  for(int x = 0; x < 800; x++) {
    digitalWrite(stepPin,HIGH); 
    delayMicroseconds(500); 
    digitalWrite(stepPin,LOW); 
    delayMicroseconds(500); 
  }
  delay(1000); // One second delay
  digitalWrite(dirPin,LOW); //Changes the direction of rotation
  for(int x = 0; x < 800; x++) {
    digitalWrite(stepPin,HIGH);
    delayMicroseconds(500);
    digitalWrite(stepPin,LOW);
    delayMicroseconds(500);
  }
  delay(1000); 
}


For wire connection, https://www.youtube.com/watch?v=BBoTkRH2E_I&ab_channel=BuildYourCNC


- It worked and the Stepper motor connection is as follow.

![image](https://github.com/princekham/cnc/assets/16104631/7470da5c-698a-47e5-8604-dacac2e09489)

![image](https://github.com/princekham/cnc/assets/16104631/99b9e9fa-984f-4e48-aeb2-5a194a060181)

I need a probe control like this : https://www.youtube.com/watch?v=kGa2s47dTss&ab_channel=JD%27sGarage

I can use the Gcode setup from here: https://www.youtube.com/watch?v=oHyvrA20QLA&ab_channel=DacVu
MS - stopping the spindle (here the torch)
M3 S1000 - starting the spindle (here the torch)
G4 P1 - waiting for one second before moving the torch


https://www.drdflo.com/pages/Guides/Plasma-Cutters-For-CNC.html

I am going to the process in setting up GRBL for cnc plasma cutting here; I will go with the check list for the completion

------------------------------------
Certainly! Setting up GRBL for CNC plasma cutting involves several steps, including configuring the firmware, connecting the hardware, and adjusting the settings. Here's a general process to get you started:

Obtain the necessary hardware:

CNC controller: You'll need a compatible CNC controller board that supports GRBL. Common options include Arduino-based boards like Arduino Uno or Arduino Mega, or specialized CNC controller boards like the CNC Shield for Arduino.
Stepper motor drivers: Choose stepper motor drivers compatible with your controller board, such as A4988 or DRV8825.
Power supply: Select an appropriate power supply to provide power to the controller board and stepper motor drivers.
Stepper motors: Use stepper motors suitable for your specific CNC plasma cutter setup.

Install GRBL firmware:

Download the latest version of GRBL firmware from the official GRBL GitHub repository (https://github.com/gnea/grbl).
Connect your CNC controller board to your computer using a USB cable.
Use the Arduino IDE or compatible software to upload the GRBL firmware to the controller board. Detailed instructions can be found in the GRBL documentation.
Configure GRBL settings:

Open a serial terminal program, such as PuTTY or CoolTerm, and connect to the serial port corresponding to your CNC controller board.
Send the "$$" command to retrieve the current GRBL settings.
Review the settings and modify them as needed. Common settings to consider for CNC plasma cutting include:

$0: Step pulse time (microseconds)
$1: Step idle delay (milliseconds)
$2: Step pulse invert (boolean)
$3: Step direction invert (boolean)
$4: Invert step enable pin (boolean)
$5: Invert limit pins (boolean)
$6: Invert probe pin (boolean)
$10: Status report options
$20: Soft limits (boolean)
$21: Hard limits (boolean)
$22: Homing cycle (boolean)
$30: Maximum spindle speed (RPM)
$31: Minimum spindle speed (RPM)
$100-$102: Steps/mm for each axis
$110-$112: Maximum rates for each axis
$120-$122: Acceleration settings for each axis
Send the modified settings to GRBL using the "$$" command.
Connect and configure peripherals:

Connect your stepper motor drivers to the CNC controller board according to the manufacturer's instructions.

Connect your limit switches to the corresponding limit switch pins on the controller board (if used).
Connect the Z-axis probe (if used) to the probe pins on the controller board.
Configure additional peripherals or accessories based on your specific CNC plasma cutter setup.
Test and calibrate:

Power on the CNC plasma cutter, ensuring that all connections are secure.
Use a G-code sender program, such as Universal Gcode Sender (UGS) or bCNC, to send G-code commands to the CNC controller and verify the motor movements.
Perform necessary calibration steps, such as homing, probing, and setting the workpiece zero position.
Please note that the specific steps and settings may vary depending on your CNC controller, hardware configuration, and plasma cutting system. It's essential to refer to the documentation provided by the manufacturers of your specific components for detailed instructions.

Always prioritize safety when working with CNC machines, and consult the user manuals and guidelines for your specific equipment throughout the setup process.

I hope this guide helps you in setting up GRBL for CNC plasma cutting!

User
How can I connect the Z-axis probe and configure it?
ChatGPT
To connect and configure a Z-axis probe for CNC plasma cutting with GRBL, you'll need to follow these general steps:

Identify the probe pins: Locate the probe pins on your CNC controller board. These pins are typically labeled and designated for connecting the Z-axis probe.

Connect the Z-axis probe: Connect the wires from the Z-axis probe to the corresponding probe pins on the CNC controller board. The exact wiring configuration may vary depending on your specific controller board and probe. Typically, the probe has two wires: one for the probe signal and the other for the ground.

Configure GRBL for the probe:

Connect your computer to the CNC controller board using a USB cable.
Open a serial terminal program, such as PuTTY or CoolTerm, and connect to the serial port corresponding to your CNC controller board.
Send the "$$" command to retrieve the current GRBL settings.
Look for the following settings related to probing:
$6 (Probe Pin Invert): This setting determines if the probe pin signal should be inverted or not. Set it to 0 or 1 based on your probe's behavior. Try different settings if the probe doesn't trigger as expected.
$10 (Status Report Mask): Adjust this setting to enable or disable reporting of the probe status. Setting it to 1 (or higher) enables reporting.
Modify the settings if necessary, and send the updated settings to GRBL using the "$$" command.
Test the Z-axis probe:

Power on the CNC plasma cutter, ensuring all connections are secure.
Open a serial terminal program and connect to the CNC controller board.
Send the command "$22" to enable homing cycle (if it's not already enabled).
Use the G-code command "G38.2 Z-10 F100" to initiate a probe cycle. This command will move the Z-axis downwards until the probe is triggered or until it reaches a distance of 10mm from the starting position (adjust the values as needed).
Observe the response from the probe and ensure that the Z-axis movement stops and the probe signal is detected.
Fine-tune the probe settings and repeat the test as necessary until the probe operates correctly.
Please note that the specific pin assignments and settings may vary depending on your CNC controller board and Z-axis probe. Always refer to the documentation provided by the manufacturers of your specific components for accurate pin configurations and detailed instructions.

As you work with the Z-axis probe, it's important to ensure the safety of yourself and the equipment. Follow proper safety protocols and guidelines while setting up and using the CNC plasma cutter.

I hope this helps you connect and configure the Z-axis probe for CNC plasma cutting with GRBL!


- GRBL Arduino Uno pin connections - https://manuals.plus/cndy-shield/grbl-cnc-arduino-uno-manual

- For Gcode reference - https://reprap.org/wiki/G-code


- For the limit switch I will install optocouplers for them
- The datasheet is at - https://www.renesas.com/us/en/document/dst/ps2501-1-ps2501-4-ps2501l-1-ps2501l-4-data-sheet
- with the pins out as follow:
![image](https://github.com/princekham/cnc/assets/16104631/ba1b0f05-0e55-4a22-9736-607138a4d864)

For generating toolpath I will use Sheetcam Software. The tutorial is at https://www.youtube.com/watch?v=aHRTZOGh3yA&ab_channel=PREMIERPLASMA

I followed the instructions from this site for GRBL installation - https://howtomechatronics.com/tutorials/how-to-setup-grbl-control-cnc-machine-with-arduino/


