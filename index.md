# Line and Distance Tracking Car
Line tracking and distance detection come as first nature to people, but technology does it better, as with most things. I built a line-tracking and distance-detecting robot. The goal: have a robot that moves along a line and then follows an object to hop back on a different set of tracks. I am happy to report I did just that.

| **Engineer** | **School** | **Area of Interest** | **Grade** |
|:--:|:--:|:--:|:--:|
| Macy D. | Los Gatos High School | Mechanical Engineering | Incoming Senior

**Replace the BlueStamp logo below with an image of yourself and your completed project. Follow the guide [here](https://tomcam.github.io/least-github-pages/adding-images-github-pages-site.html) if you need help.**

![Headstone Image](logo.svg)
  
<!--- # Final Milestone 

**Don't forget to replace the text below with the embedding for your milestone video. Go to Youtube, click Share -> Embed, and copy and paste the code to replace what's below.**

<iframe width="560" height="315" src="https://www.youtube.com/embed/F7M7imOVGug" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

 For your final milestone, explain the outcome of your project. Key details to include are:
- What you've accomplished since your previous milestone
- What your biggest challenges and triumphs were at BSE
- A summary of key topics you learned about
- What you hope to learn in the future after everything you've learned at BSE --->



# Second Milestone

<iframe width="560" height="315" src="https://www.youtube.com/embed/a9T-wzgI77I" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

The second milestone, for me, consisted of learning how to write my own code. I used the code from the blink test and an "if" statement to make the LED blink when on a dark surface with the line track bottom sensor. All concepts I used were utterly foreign to me before this milestone. Then I combined the ideas from the motor test run, a sample from a follow-line test, and the sensor run to try and make the robot move on the line. I had trouble getting the bot to follow along sharp curves once I got it to follow the initial semi-straight line. For a while, it only went one way, but then I found out that by using multiple if statements with the combination of the left and right sensors, it could turn back once off the line. As was the initial issue, I had to ensure that once off the line, the car would turn instead of head straight forward. I then created a looped track, and the bot successfully followed the black line in both directions. 


# First Milestone

<iframe width="560" height="315" src="https://www.youtube.com/embed/dDlCzctv_jg" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

My first milestone was assembling my build and running test code to ensure the motors ran. I ran into a few issues with the TB6612 motor driver. After a few tries, I could upload the code after switching from cam mode to upload mode on my Arduino uno board. The bot moves forward, backward, then side to side after running the motor test run in the SparkFun TB6612FNG Motor Drive Library. 

<!--- # Schematics --->
<!--- Here's where you'll put images of your schematics. [Tinkercad] (https://www.tinkercad.com/blog/official-guide-to-tinkercad-circuits) and [Fritzing](https://fritzing.org/learning/) are both great resoruces to create professional schematic diagrams, though BSE recommends Tinkercad becuase it can be done easily and for free in the browser. --->

# Code

```c++
#include <SimpleUltrasonic.h>
#include <Servo.h>
#include <SparkFun_TB6612.h>

#define AIN1 7
#define BIN1 8
#define AIN2 1
#define BIN2 2
#define PWMA 5
#define PWMB 6
#define STBY 3
#define R_S A0 //ir sensor Right
#define L_S A2 //ir sensor Left
#define M_S A1 //ir senoe middle
const int offsetA = 1;
const int offsetB = 1;
Motor motor1 = Motor(BIN1, BIN2, PWMB, offsetB, STBY);
Motor motor2 = Motor(AIN1, AIN2, PWMA, offsetA, STBY);
const int lineTrack = A0;

Servo servo;    
const int trigPin = 13;
const int echoPin = 12;  
const int servoPin = 10;

SimpleUltrasonic sensor(trigPin, echoPin);

int scanAngle = 0;              // Initial servo scanning angle
int pos = 0;
int distance [180];

const int minServoAngle = 0;    // Minimum angle of the servo
const int maxServoAngle = 180;  // Maximum angle of the servo
const int maxTurnTime = 1460;   // Time (in milliseconds) to turn 90 degrees


void setup() {
  Serial.begin(9600);
  pinMode(lineTrack, INPUT);
  servo.attach(servoPin);       // Attach servo to the servo pin
  servo.write(scanAngle);       // Set servo to initial angle
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);
  delay(1000);
}

void loop() {                         
  int sensorValue = analogRead(A1);
  int speed = 120;     
  int shortestDistance = 9999;
  int shortestAngle = 0;
  int distance = sensor.measureDistanceInCM();
  
  Serial.println(sensorValue);                           //when the sensor output is above 600 then it is on the line
  if((analogRead(R_S) > 600)&&(analogRead(L_S) > 600)){  //this was for when the track was wide enough to reach both sides, not always in use
    forward(motor1, motor2, 100);}
  if(analogRead(M_S) > 600){                             //"<" = off the line, ">" = on the line
    forward(motor1, motor2, 100);}                                                                              
  if((analogRead(R_S) < 600)&&(analogRead(L_S) > 600)){  //if off track on the right it will trun twards the left
    left(motor1, motor2, 100);}
  if((analogRead(R_S) > 600)&&(analogRead(L_S) < 600)){
    right(motor1, motor2, 100);}
  if((analogRead(M_S) < 600)&&(analogRead(R_S) < 600)&&(analogRead(L_S) < 600)){    //just in case it gets off track
      brake(motor1, motor2);
      for (int angle = 0; angle <= 180; angle += 10) {  // Scan every 10 degrees withing 180 degrees
      servo.write(angle);
      delay(500); 
     
      Serial.print("Angle: ");
      Serial.print(angle);
      Serial.print(" degrees, Distance: ");
      Serial.print(distance);
      Serial.println(" cm");
                                                           // Check if this distance is shorter than the previous shortest distance
     if (distance != -1 && distance < shortestDistance) {   // check if -1, becuase that is an invalid reading, will not include as shortest
      shortestDistance = distance;                         // then it becomes shortest distance 
      shortestAngle = angle;                               // and shortest angle
    }    
    }
    servo.write(shortestAngle);          // Turn the servo head towards the shortest distance, defined above
    Serial.print("Shortest distance: "); // Print the shortest distance
    Serial.print(shortestDistance);
    Serial.println(" cm");
    
    int mappedLeftTurnTime = map(abs(shortestAngle - 90), 0, 90, 1460, 0);
    int mappedRightTurnTime = map(abs(90 - shortestAngle ), 0, 90, 0, 1460);
    
    if (shortestAngle < 90){              // if the shortest angle is < 90 then it will turn towards the right 
     right(motor1, motor2, 100);
     delay(mappedRightTurnTime);
    } else {
     left(motor1, motor2, 100);
     delay(mappedLeftTurnTime);
     }                                      // Wait for 4 seconds at the shortest distance
     forward(motor1, motor2, 100);
     delay(500);
     brake();                                 // Stop both motors
     delay(2000);                           // if the shortest angle is > 90 then it will turn towards the left  
  }
  } 
  void brake() {
  motor1.brake();
  motor2.brake();
  }  
```

# Bill of Materials 

| **Part** | **Note** | **Price** | **Link** |
|:--:|:--:|:--:|:--:|
| Smart Robot Car V4.0 | Main Build | $79.99 | <a href="https://www.amazon.com/ELEGOO-Tracking-Ultrasonic-Intelligent-Educational/dp/B07KPZ8RSZ"> Link </a> |

# Other Resources/Examples
- [Sparkfun Library](https://github.com/sparkfun/SparkFun_TB6612FNG_Arduino_Library)
- [Simple Ultrasonic](https://github.com/gamegine/HCSR04-ultrasonic-sensor-lib)
- [Line Following Example Code](https://circuitdigest.com/microcontroller-projects/arduino-uno-line-follower-robot)
- [Sun Founder](https://docs.sunfounder.com/projects/sensorkit-v2-arduino/en/latest/lesson_35.html)
