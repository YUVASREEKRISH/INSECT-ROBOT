# INSECT-ROBOT
This robot detects the object via ultrasonic sensor and moves along a new path.The future application of this robot is implementing it in military fields by using metal detecting sensors.
CENTERING THE SERVO
#include<Servo.h>
Servo myServo;
void setup()
{
myServo.attach(2);
myServo.write(90);
}
void loop()
{
delay(100);
}
MOVING THE SERVO
#include<Servo.h>
Servo myServo;
int delayTime=1000;
void setup()
{
myServo.attach(2);
}
void loop()
{
myServo.write(90);
delay(delayTime);
myServo.write(180);
delay(delayTime);
myServo.write(90);
delay(delayTime);
myServo.write(0);
delay(delayTime);
}
CENTERING 2 SERVO
#include<Servo.h>
Servo frontServo;
Servo rearServo;
void setup()
{
frontServo.attach(2);
rearServo.attach(3);
frontServo.write(90);
rearServo.write(90);
}
void loop()
{
delay(100);
}
WALKING FORWARD
#include<Servo.h>
Servo frontServo;
int centerPos=90;
int frontRightUp=72;
int frontLeftUp=108;
int backRightForward=75;
int backLeftForward=105;
void moveForward()
{
frontServo.write(frontRightUp);
rearServo.write(backLeftForward);
delay(125);
frontServo.write(centerPos);
rearServo.write(centerPos);
delay(65);
frontServo.write(frontLeftUp);
rearServo.write(backRightForward);
delay(125);
frontServo.write(centerPos);
rearServo.write(centerPos);
delay(65);
}
void setup()
{
frontServo.attach(2);
rearServo.attach(3);
}
void loop()
{
moveForward();
delay(150);
}
WALKING BACKWARD
void moveBackward()
{
frontServo.write(frontRightUp);
rearServo.write(backRightForward);
delay(125);
frontServo.write(centerPos);
rearServo.write(centerPos);
delay(65);
frontServo.write(frontLeftUp);
rearServo.write(backLeftForward);
delay(125);
frontServo.write(centerPos);
rearServo.write(centerPos);
delay(65);
}
TURNING BACKWARD
void mainBackRight()
{
frontServo.write(frontRightUp);
rearServo.write(backRightForward-6);
delay(65);
frontServo.write(frontLeftUp+9);
rearServo.write(backLeftForward-6);
delay(125);
frontServo.write(centerPos);
rearServo.write(centerPos);
delay(65);
}
TURNING FORWARD
void moveTurnLeft()
{
frontServo.write(frontTurnRightUp);
rearServo.write(backTurnLeftForward);
delay(125);
frontServo.write(centerTurnPos);
rearServo.write(centerTurnPos);
delay(65);
frontServo.write(frontTurnLeftUp);
rearServo.write(backTurnRightForward);
delay(125);
frontServo.write(centerTurnPos);
rearServo.write(centerTurnPos);
delay(65);
}
ATTACHING THE ULTRASONIC SENSOR

MEASURING DISTANCE USING PING
long distanceCm()
{
pinMode(pingPin,OUTPUT);
digitalWrite(pingPin,LOW);
delayMicroseconds(2);
digitalWrite(pingPin,HIGH);
delayMicroseconds(5);
digitalWrite(pingPin,LOW);
pinMode(pingPin,INPUT);
duration=pulseIn(pingPin,HIGH);
distanceInches=microsecondsToInches(duration);
return microsecondsToCentimeters(duration);
}
int pingPin=4;
long int duration,distanceInches;
long distanceFront=0;//cm
int startAvoidanceDistance=20;//cm
long microsecondsToInches(long microseconds)
{
return microseconds/74/2;
}
long microsecondsToCentimeters(long microseconds)
{
return microseconds/29/2;
}
void loop()
{
distanceFront=distanceCm();//filters out any stray 0.00 error readings
if(distanceFront>1)
{
if(distanceFront<startAvoidanceDistance)
{
for(int i=0;i<=8;i++)
{
moveBackRight();
delay(walkSpeed);
}
for(int i=0;i<=10;i++)
{
moveTurnLeft();
delay(walkSpeed);
}
}
else
{
moveForward();
delay(walkSpeed);
}
}
}

