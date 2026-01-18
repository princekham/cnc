# Router CNC
### GRBL File of my machine

```
$0=10
$1=25
$2=0
$3=1
$4=0
$5=1
$6=0
$10=1
$11=0.010
$12=0.002
$13=0
$20=0
$21=1
$22=1
$23=3
$24=100.000
$25=200.000
$26=44
$27=5.000
$30=1000
$31=0
$32=0
$100=1289.000
$101=1289.000
$102=1289.000
$110=500.000
$111=500.000
$112=250.000
$120=10.000
$121=10.000
$122=10.000
$130=85.000
$131=175.000
$132=85.000
```

## Wire Connection
(source: https://www.youtube.com/watch?v=fyH5hU6ctvw)
Digital Pin 8 is 'stepper motors enable' pins
<img width="894" height="698" alt="image" src="https://github.com/user-attachments/assets/1283ca84-29f6-4ee0-a936-10f7eb854901" />

Step Direction Pins
- For X : 2 (step), 5(dir)
- For Y : 3, 6
- For Z : 4, 7
- For extruder : not directly connected to Arduino

<img width="894" height="600" alt="image" src="https://github.com/user-attachments/assets/78420558-7ba1-4f3c-b754-f095bd62dd87" />

- Ground pins
  <img width="894" height="596" alt="image" src="https://github.com/user-attachments/assets/e2d5106e-8fd2-48cf-9fdf-42e71fc65587" />
- Digital 12 : Spindle En
- Digital 13 : Spindle Dir
- Limit X+,X- : Digital 9
- Limit Y+,Y- : Digital 10
- Limit Z+,Z- : Digital 11
- Abort : A0
- Hold : A1
- Resume : A2
- CoolEn : A3 (Digital 17)
- SDA : A4 (Digital 18)
- SCL : A5 (Digital 19)
- Rx : Digital 0
- Tx : Digital 1
  <img width="1793" height="1012" alt="image" src="https://github.com/user-attachments/assets/6097e427-3e81-41f8-9182-b3e6dc855cc1" />

  ### Probe Connection
  - probe pin is SCL (A5) and GND (according to Google AI)
  ### Notes on Z+,Z- Limit
  - For all versions of GRBL v0.9 and higher (including current v1.1), the Z-limit pin and Spindle Enable pin were swapped to allow for variable spindle speed (PWM).
  - The Solution: You must connect your Z-axis limit switch to the header labeled SpnEn (Spindle Enable) instead of the Z+/- header, or reflash your firmware to disable VARIABLE_SPINDLE.

## Running the machine
- terminal commands
- '$' for help
- '$$' for config settings

  
### BCNC
- https://github.com/vlachoudis/bCNC
- to run BCNC
  ```python -m bCNC```

### Router Bits
- 30 degree
- 0.1x30DEGx3.175x38
<img width="400" height="889" alt="image" src="https://github.com/user-attachments/assets/3c2b62f3-a560-4682-b472-4ef6ea270592" />

### For Drilling
- drill pin size 
