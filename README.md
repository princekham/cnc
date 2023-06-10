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

- It worked.
