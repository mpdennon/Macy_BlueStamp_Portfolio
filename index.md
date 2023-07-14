# Line and Distance Tracking Car
Line tracking and distance detection come as first nature to people, but technology does it better, as with most things. I built a line-tracking and distance-detecting robot. The goal: have a robot that moves along a line and then follows an object to hop back on a different set of tracks. I am happy to report I did just that.

| **Engineer** | **School** | **Area of Interest** | **Grade** |
|:--:|:--:|:--:|:--:|
| Macy D. | Los Gatos High School | Mechanical Engineering | Incoming Senior

**Replace the BlueStamp logo below with an image of yourself and your completed project. Follow the guide [here](https://tomcam.github.io/least-github-pages/adding-images-github-pages-site.html) if you need help.**

![Headstone Image](logo.svg)
  
<!--- # Final Milestone --->

**Don't forget to replace the text below with the embedding for your milestone video. Go to Youtube, click Share -> Embed, and copy and paste the code to replace what's below.**

<iframe width="560" height="315" src="https://www.youtube.com/embed/F7M7imOVGug" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

For your final milestone, explain the outcome of your project. Key details to include are:
- What you've accomplished since your previous milestone
- What your biggest challenges and triumphs were at BSE
- A summary of key topics you learned about
- What you hope to learn in the future after everything you've learned at BSE



# Second Milestone

**Don't forget to replace the text below with the embedding for your milestone video. Go to Youtube, click Share -> Embed, and copy and paste the code to replace what's below.**

<iframe width="560" height="315" src="https://www.youtube.com/embed/y3VAmNlER5Y" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

The second milestone, for me, consisted of learning how to write my own code. I used the code from the blink test and an "if" statement to make the LED blink when on a dark surface with the line track bottom sensor. All concepts I used were utterly foreign to me before this milestone. Then I combined the ideas from the motor test run, a sample from a follow-line test, and the sensor run to try and make the robot move on the line. I had trouble getting the bot to follow along sharp curves once I got it to follow the initial semi-straight line. For a while, it only went one way, but then I found out that by using multiple if statements with the combination of the left and right sensors, it could turn back once off the line. I had to ensure that once off the line, the car would turn instead of head straight forward, as was the initial issue. I then created a looped track, and the bot successfully followed the black line in both directions. 


# First Milestone

<iframe width="560" height="315" src="https://www.youtube.com/embed/dDlCzctv_jg" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

My first milestone was assembling my build and running test code to ensure the motors ran. I ran into a few issues with the TB6612 motor driver. After a few tries, I could upload the code after switching from cam mode to upload mode on my Arduino uno board. The bot moves forward, backward, then side to side after running the motor test run in the SparkFun TB6612FNG Motor Drive Library. 

<!--- # Schematics --->
<!--- Here's where you'll put images of your schematics. [Tinkercad] (https://www.tinkercad.com/blog/official-guide-to-tinkercad-circuits) and [Fritzing](https://fritzing.org/learning/) are both great resoruces to create professional schematic diagrams, though BSE recommends Tinkercad becuase it can be done easily and for free in the browser. --->

<!--- # Code --->
<!--- Here's where you'll put your code. The syntax below places it into a block of code. Follow the guide [here]([url](https://www.markdownguide.org/extended-syntax/)) to learn how to customize it to your project needs. --->

```c++
void setup() {
  // put your setup code here, to run once:
  Serial.begin(9600);
  Serial.println("Hello World!");
}

void loop() {
  // put your main code here, to run repeatedly:

}
```

# Bill of Materials 

| **Part** | **Note** | **Price** | **Link** |
|:--:|:--:|:--:|:--:|
| Smart Robot Car V4.0 | Main Build | $79.99 | <a href="https://www.amazon.com/ELEGOO-Tracking-Ultrasonic-Intelligent-Educational/dp/B07KPZ8RSZ"> Link </a> |

# Other Resources/Examples
- [whatever code I end up using](https://trashytuber.github.io/YimingJiaBlueStamp/)
- [Line Following Example Code](https://circuitdigest.com/microcontroller-projects/arduino-uno-line-follower-robot)
- [Sun Founder][https://docs.sunfounder.com/projects/sensorkit-v2-arduino/en/latest/lesson_35.html]
