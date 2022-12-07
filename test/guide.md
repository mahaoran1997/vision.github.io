---
sort: 1
---

# Step-by-step Guide


## 1 Hardware Setup
### 1.1 Required Components:
* ESP8266 NodeMCU
* Arduino Uno
* L298N Motor Driver
* WS2812B RGB LEDS
* 12V DC Motor
* 3.7V 400mA Lithium Battery
* 12V Battery (Power the motor)
* 330<span>&#8486;</span> Resistor
* 18cm &#xD7; 10cm PCB Board
* 4mm Rigid Flange
* Screws and Nuts

### 1.2 Circuit Schematics:
The first scheme is ESP8266 circuit, which powers the WS2812 LEDs and uses WiFi to control and switch the light patterns.
<img src="https://www.haoranma.info/vision.github.io/assets/images/NodeMCU Circuit_schem.jpg" alt="ESP8266 Circuit Scheme">
<p>
The following picture is the L298N Motor Driver Scheme, which powers the 12V motor and controls the motor's rotational speed. 
<img src="https://www.haoranma.info/vision.github.io/assets/images/Motor Circuit_bb.png" alt="L298N Motor Driver Scheme">
<p>
To power and control the motor speed, we need to use the Pulse Width Modulation (PWM), a way to control analog devices with a digital output. In other words, we can output a modulating signal from a digital device (Arduino Uno) to drive an analog device (motor). After setting up the motor driver circuit, we can simply assign the Arduino output pins, and call `analogWrite`

```C++
int enA = 9;
int in1 = 8;
int in2 = 7;

void setup() {
  pinMode(enA, OUTPUT);
  pinMode(in1, OUTPUT);
  pinMode(in2, OUTPUT);

}

void loop(){
  digitalWrite(in1,HIGH);
  digitalWrite(in2,LOW);

  analogWrite(enA,321);

  delay(2000);
  digitalWrite(in1,LOW);
  digitalWrite(in2,HIGH);
}
```

### 1.3 3D Printed Models:
* The following two models are 3D printed to contain all the required components, the original STL files can be found <a href="https://github.com/mahaoran1997/vision.github.io/tree/develop/assets/3D%20Models" target="_blank">here</a>.
<table>
<tr><td><center>Model Base</center></td><td> <center>Model Cover</center></td></tr>
<tr><td>
<img align="center" src="https://www.haoranma.info/vision.github.io/assets/images/Model Base.png" alt="Model Base"/></td><td> <img align="center" src="https://www.haoranma.info/vision.github.io/assets/images/Model Cover.png" alt="Model Cover"/></td></tr>
</table>

## 2 Software Code

Here we show how to use our POVLib to easily build a POV Display and a web server.

### 2.1 Web Server

To build a simple web server, we need to firstly import the html module of our POVLib. And then declare an object with class `TemplateHtml`. Inside the setup function, we initialize the TemplateHtml object with parameters specified by us.

```C++
#include <html.h>

TemplateHtml our_html;
void setup() {    
  Serial.begin(115200);
  // .....
  TemplateHtml::initialize(5, texts, wifi_ssid, wifi_password, &current_pattern, text_s);
}
```
In the code above, we input 6 parameters into the initialize function. The first parameter is how many patterns we have. The second parameter is a string array. It contains the pattern names. The third and fourth parameters are the ssid and password of wifi server specified by users. The fifth parameter is an integer pointer, it is used to transfer the information of pattern selected by users from html module to our code. The last parameter is a char array and is also used to transfer parameter information from html module to our code (e.g. the input box shown in section 3).

Then at the start of the loop function, we need to call `TemplateHtml::handle_client()`. 
```C++
void loop() {
  TemplateHtml::handle_client();
  // Code to show patterns ...
}
```


### 2.2 Create Patterns

To easily create our patterns using POVLib, we need to firstly import the pov module of our POVLib. And then create an object with class `POVLib`. Inside the setup function, we call the constructor of POVLib.
```C++
#include <pov.h>

POVLib* pov;
void setup() {    
  Serial.begin(115200);
  // .....
  pov = new POVLib(LED_PIN, NUM_LEDS, BRIGHTNESS, SPEED, NUM_INTERVALS, LED_TYPE, COLOR_ORDER);
  pov->reset();
}
```
In the code above, we input 7 parameters into the constructor of POVLib. The first parameter is the pin number of LED. The second parameter is the number of leds we have on the stripe. The third specifies the brightness of LED and the fourth parameter specifies the speed of the motor. The fifth parameter is how many intervals we want to split for a single circle. The last two parameters are the type of our leds and the color order.

So basically the POVLib will create a polar grid graph. There are NUM_LEDS*NUM_INTERVALS points in the graph. And we use (Interval ID, LED ID) to identify each point. The `reset` function just resets every point to black. We can use other interfaces to create patterns we want. A complete interface introduction can be found in [section 2](https://www.haoranma.info/vision.github.io/test/modules.html). Here we show an example: how we created our shape pattern.

```C++
void loop() {
  TemplateHtml::handle_client();
  // ...
  else if (current_pattern == 4) {
    show_shape();
  }
  // Other patterns ...
}

unsigned int povcolors[4] = {CRGB::Red, CRGB::Blue, CRGB::Green, CRGB::Yellow};
void show_shape() {
  EVERY_N_SECONDS(1) {
    for (int i = 0; i < NUM_INTERVALS; i += 3) {
      for (int j = 0; j < 3; j ++) {
        pov->draw_curve(i, (i + 3) % NUM_INTERVALS, j, povcolors[i/3]);
      }
      pov->draw_curve((i + 1) % NUM_INTERVALS, (i + 4)%NUM_INTERVALS, 3, povcolors[i/3]);
      pov->draw_curve((i + 2) % NUM_INTERVALS, (i + 5)%NUM_INTERVALS, 4, povcolors[i/3]);
      pov->draw_curve((i + 2) % NUM_INTERVALS, (i + 5)%NUM_INTERVALS, 5, povcolors[i/3]);
      pov->draw_curve((i + 2) % NUM_INTERVALS, (i + 5)%NUM_INTERVALS, 6, povcolors[i/3]);
      pov->draw_curve((i + 1) % NUM_INTERVALS, (i + 4)%NUM_INTERVALS, 7, povcolors[i/3]);
      for (int j = 8; j < 11; j ++) {
        pov->draw_curve(i, (i + 3) % NUM_INTERVALS, j, povcolors[i/3]);
      }
    }
  }
  pov->run_loop_body();
}
```
In the loop function, we check the value of `current_pattern`. If it is 4, then we call `show_shape` to show the pattern we create. In `show_shape`, we firstly draw the pattern. The `draw_curve` function takes four input parametes. The first two specifies the start and end interval IDs of this curve and the third parameter specifies the LED ID of the curve. The last one gives the color of this curve. Actually We can also draw dots and lines using other interfaces. After creating the pattern, we need to call the `run_loop_body` function in POVLib to let our hardwares show the pattern.

## 3 Visual Effects

We built a demo system and created five different patterns using our library to show its usability. Our demo system has a web interface, and users can select which pattern to show on our led display through buttons on the webpage. To open the webpage, users firstly need to connect to the wifi channel created by our system and goto `192.168.4.1` in your browser app. The web page is shown below and we can see five different patterns on the website. 

<center>
<figure>
<figcaption align = "center"><b>Demo Web Page</b></figcaption>
<img align="center" src="https://www.haoranma.info/vision.github.io/assets/images/WebPage.PNG" alt="Demo Web Page" width="400"/>
</figure>
</center>



### 3.1 Color Pattern
After we activate the first pattern -- color pattern which is the simplest one in this demo. It changes its color every 5 seconds. The visual effects are shown below:

<table>
<tr><td><center>Color Pattern 1</center></td><td> <center>Color Pattern 2</center></td></tr>
<tr><td>
<img align="center" src="https://www.haoranma.info/vision.github.io/assets/images/pattern1_1.JPG" alt="Color Pattern 1"/></td><td> <img align="center" src="https://www.haoranma.info/vision.github.io/assets/images/pattern1_2.JPG" alt="Color Pattern 2"/></td></tr>
</table>

We used long exposure camera to capture the pattern. Due to the camera sampling frequency is not high enough, though the pattern in the image is missing a corner, it actually fills all round face when we are looking at it through our eyes. This problem also arises in the rest several patterns.

### 3.2 Clock Pattern
After we activate the second pattern -- clock pattern. It shows the current time (hour and minute). The visual effects are shown below:


<table>
<tr><td><center>Clock Pattern 1</center></td><td> <center>Clock Pattern 2</center></td></tr>
<tr><td>
<img align="center" src="https://www.haoranma.info/vision.github.io/assets/images/pattern2_1.JPG" alt="Clock Pattern 1"/></td><td> <img align="center" src="https://www.haoranma.info/vision.github.io/assets/images/pattern2_2.JPG" alt="Clock Pattern 2"/></td></tr>
</table>




### 3.3 Circle Pattern
After we activate the third pattern -- circle pattern. It shows a circle starting from inner side gradually goes to outer side. The visual effects are shown below:

<table>
<tr><td><center>Circle Pattern 1</center></td><td> <center>Circle Pattern 2</center></td><td> <center>Circle Pattern 3</center></td></tr>
<tr><td>
<img align="center" src="https://www.haoranma.info/vision.github.io/assets/images/pattern3_1.JPG" alt="Circle Pattern 1"/></td><td> <img align="center" src="https://www.haoranma.info/vision.github.io/assets/images/pattern3_2.JPG" alt="Circle Pattern 2"/></td><td> <img align="center" src="https://www.haoranma.info/vision.github.io/assets/images/pattern3_3.JPG" alt="Circle Pattern 3"/></td></tr>
</table>


### 3.4 Shape Pattern
After we activate the fourth pattern -- shape pattern. It shows the a complex colorful pattern designed by us using less than 10 lines of code. The visual effects are shown below:

<table>
<tr><td><center>Shape Pattern 1</center></td><td> <center>Shape Pattern 2</center></td></tr>
<tr><td>
<img align="center" src="https://www.haoranma.info/vision.github.io/assets/images/pattern5_1.jpg" alt="Shape Pattern 1"/></td><td> <img align="center" src="https://www.haoranma.info/vision.github.io/assets/images/pattern5_2.JPG" alt="Shape Pattern 2"/></td></tr>
</table>


### 3.5 Text Pattern
After we input the text we want to show into the text box and submit it, it activates the last pattern -- text pattern. It shows the texts specified by us. Example visual effects are shown below (we use "hello" as an example):

<center>
<figure>
<figcaption align = "center">Text Pattern</figcaption>
<img align="center" src="https://www.haoranma.info/vision.github.io/assets/images/pattern4.jpg" alt="Text Pattern" width="500"/>
</figure>
</center>