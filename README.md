# cnc
Notes on my CNC plasma table

Limit Switch one to IN1 and the other to ground

Stepper motor driver setup
- Ampere requirement according to Nema 23 specs is 2.8 A, so I will set it to 3.31A which is off, on, off for switch 1,2,3
- For microstepping 3200 is chosen which is on on off on for switch 5, 6, 7, 8
- switch 4 is off for Half current
