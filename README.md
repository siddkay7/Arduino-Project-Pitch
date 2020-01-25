# Arduino-Project-Pitch
Arduino Project Pitch- An integrated device consisting of a speed gun and a Breathalyzer.

Problem Statement :
Inability of policemen to manage and record crimes easily and use technology. 

Solution:
I have made an integrated device which can act as both a Speed Gun as well as a Breathalyzer. The components I have used are : 
Ultrasonic sensor(for Speed gun), an IR blaster (for Breathalyzer which is actually a modified IR spectrometer), a bluetooth HC-05 device, led. and an arduino. When Overspeed or Alcohol is detected, a message is sent to the phone which in turn can be directly recorded and an LED turns on. Therefore it serves a dual purpose and is also linked to a mobile device. Thus data is recorded.

Code: 

void breathalyzer();
void speedgun();
const int trigPin=9;
const int echoPin=10;
#define led 13
#define ir 6
long duration;
int distance;
void setup() {
  pinMode(trigPin,OUTPUT);
  pinMode(echoPin,INPUT);
  pinMode(led,OUTPUT);
  pinMode(ir,INPUT);
  Serial.begin(9600);
  
  
  // put your setup code here, to run once:

}

void loop() {
  digitalWrite(led,0);
  Serial.println("Press 1 for Breathalyzer and 2 for Speed Gun");
              delay(7000);
  if(Serial.available())
  {
   char ch=Serial.read();
   if(ch=='1')
  breathalyzer();
  else if(ch=='2')
  speedgun();
  }
  
 }
 void speedgun()
 {
  digitalWrite(trigPin,LOW); //next 5 lines have to be written coz manufacturer insists.
  delayMicroseconds(2);

  digitalWrite(trigPin,HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin,LOW);
  int duration1,duration2,distance1,distance2;
  duration1=pulseIn(echoPin,HIGH);
  delay(1000);
  duration2=pulseIn(echoPin,HIGH);
  
  distance1=duration1*0.034/2;
  distance2=duration2*0.034/2;
  int speed=(distance1-distance2)/1; //Due to limitations, speed gun is assumed to be in front of the vehicle as it approaches.
  Serial.print("The speed is ");
  Serial.println(speed);

  if(speed>60)
  digitalWrite(led,1);
  else
  digitalWrite(led,0);

  }
 void breathalyzer()
  {
    int n=analogRead(ir);
    Serial.print("\nThe reading is ");
    Serial.print(n);
    if(n>250)
    {
    Serial.println("\nAccording to value, person gets arrested.");
    digitalWrite(led,1);
    delay(4000);
    }
    else
    {
      digitalWrite(led,0);
    Serial.println("\nAccording to value, person is not arrested.");
    }
  }  
  
  
  
  
 



