# **SMART-PEDESTRIAN-CROSSING-SYSTEM**
This project involves the use of IR sensors and a real-time monitoring system to detect pedestrians and control traffic signals. As the signal changes, pop-up barricades are activated to manage the movement of vehicles and pedestrians, making crossings safer and improving traffic flow.
## AIM
To enhance pedestrian safety, improve traffic efficiency, and create a more visible and responsive crosswalk system through real-time monitoring and smart control technologies.
## COMPONENTS
1. Arduino UNO
2. IR sensor
3. Servo motor
4. Relay module
5. LED driver
6. LED
## BLOCK DIAGRAM

![blockdiagram](https://github.com/EmildaBabu/pedestrian-crossing-system/blob/76f119826ea9ddd5493840dd3e08ced00e4e9d4c/blockdiagram.JPG)

## LINKEDIN
[Working demo](https://www.linkedin.com/posts/emildababu_smart-pedestrian-crossing-the-smart-pedestrian-activity-7294728905268080642-HXuT?utm_source=share&utm_medium=member_android&rcm=ACoAAESb094BLLgjC4CNOMXZxE2eOt9Lr_BX71E)

## CODE
Platform : Arduino IDE

```cpp
#include <Servo.h>

const int ir1=4;
const int ir2=3;

const unsigned long interval=20000;
unsigned long previoustime=0;

const int servoped=5;
const int servocent=6;
const int servoside=7;

const int redLedPin =8;
const int greenLedPin =9;
const int centrewhiteLedPin =10;
const int sidewhiteLedPin =11;

Servo pedmot;
Servo centmot;
Servo sidemot;

int ircount1=0;
int ircount2=0;


void setup()
 {
 
    pinMode(ir1,INPUT);
    pinMode(ir2,INPUT);
    pinMode(greenLedPin,OUTPUT);
    pinMode(redLedPin,OUTPUT);
    pinMode(centrewhiteLedPin,OUTPUT);
    pinMode(sidewhiteLedPin,OUTPUT);

    pedmot.attach(servoped);
    centmot.attach(servocent);
    sidemot.attach(servoside);

    Serial.begin(9600);

    digitalWrite(redLedPin,LOW);
    digitalWrite(greenLedPin,HIGH);
    digitalWrite(centrewhiteLedPin,HIGH);
    digitalWrite(sidewhiteLedPin,HIGH);

    pedmot.write(170);
    centmot.write(20);
    sidemot.write(90);

}

void loop()
{

  int ir1State = digitalRead(ir1);
  int ir2State = digitalRead(ir2);

  unsigned long currenttime=millis();

  if(ir1State == LOW)
  {
    ircount1++;
    delay(1000);
    Serial.print("count of 1:");
    Serial.println(ircount1);

    if(ircount1 >= 5)
    {
    sidemot.write(180);
    pedmot.write(70);
    digitalWrite(redLedPin,HIGH);
    digitalWrite(greenLedPin,LOW);
    digitalWrite(centrewhiteLedPin,LOW);
    digitalWrite(sidewhiteLedPin,LOW);
    delay(2000);
    }
    else if(ircount1<5)
    {
      if(currenttime - previoustime >=interval)
      {
      centmot.write(120);
      pedmot.write(70);
      digitalWrite(redLedPin,HIGH);

      digitalWrite(greenLedPin,LOW);
      digitalWrite(centrewhiteLedPin,LOW);
      digitalWrite(sidewhiteLedPin,HIGH);
      }
    }
  }
  if(ir2State == LOW)
  {
    ircount2++;
    delay(1000);
    Serial.print("count:");
    Serial.println(ircount2);
    if(ircount1==ircount2)
    {
      ircount1=0;
      ircount2=0;

      digitalWrite(redLedPin,LOW);
      digitalWrite(greenLedPin,HIGH);
      digitalWrite(centrewhiteLedPin,HIGH);
      digitalWrite(sidewhiteLedPin,HIGH);

      pedmot.write(170);
      centmot.write(20);
      sidemot.write(90);

      millis()==0;

    }
  }
}
```
## OUTPUT
<p align="center">
  <img src="https://github.com/EmildaBabu/pedestrian-crossing-system/blob/151d5abf16db7db661b0e526b48675c8b2358be2/During%20Normal%20time.jpg?raw=true" alt="Image 1" width="500"/>
</p>

<p align="center">
  <img src="https://github.com/EmildaBabu/pedestrian-crossing-system/blob/3eb349cc3908085e6c0353d9c35bfa6edf4ed7e5/when%20the%20vehicles%20passing.jpg?raw=true" alt="Image 2" width="500"/>
</p>
