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
* The first scheme is ESP8266 circuit, which powers the WS2812 LEDs and uses WiFi to control and switch the light patterns.
<img src="https://www.haoranma.info/vision.github.io/assets/images/NodeMCU Circuit_schem.jpg" alt="ESP8266 Circuit Scheme">
* The following picture is the L298N Motor Driver Scheme, which powers the 12V motor and controls the motor's rotational speed. 
<img src="https://www.haoranma.info/vision.github.io/assets/images/Motor Circuit_bb.png" alt="L298N Motor Driver Scheme">

### 1.3 3D Printed Models:
* The following two models are 3D printed to contain all the required components, the original STL files can be found <a href="https://github.com/mahaoran1997/vision.github.io/tree/develop/assets/3D%20Models" target="_blank">here</a>.
<img src="https://www.haoranma.info/vision.github.io/assets/images/Model Base.png" alt="Model Base">
<img src="https://www.haoranma.info/vision.github.io/assets/images/Model Cover.png" alt="Model Cover">

## 2 Software Code



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
<tr><td>![Color Pattern 1](https://www.haoranma.info/vision.github.io/assets/images/pattern1_1.JPG) </td><td> ![Color Pattern 2](https://www.haoranma.info/vision.github.io/assets/images/pattern1_2.JPG)</td></tr>
</table>

We used long exposure camera to capture the pattern. Due to the camera sampling frequency is not high enough, though the pattern in the image is missing a corner, it actually fills all round face when we are looking at it through our eyes. This problem also arises in the rest several patterns.

### 3.2 Clock Pattern
After we activate the second pattern -- clock pattern. It shows the current time (hour and minute). The visual effects are shown below:


<center>Clock Pattern 1</center>| <center>Cclock Pattern 2</center>
--- | ---
![Clock Pattern 1](https://www.haoranma.info/vision.github.io/assets/images/pattern2_1.JPG) | ![Clock Pattern 2](https://www.haoranma.info/vision.github.io/assets/images/pattern2_2.JPG)




### 3.3 Circle Pattern
After we activate the third pattern -- circle pattern. It shows a circle starting from inner side gradually goes to outer side. The visual effects are shown below:


<center>Circle Pattern 1</center>| <center>Circle Pattern 2</center> | <center>Circle Pattern 3</center>
--- | --- | ---
![Circle Pattern 1](https://www.haoranma.info/vision.github.io/assets/images/pattern3_1.JPG) | ![Circle Pattern 2](https://www.haoranma.info/vision.github.io/assets/images/pattern3_2.JPG) | ![Circle Pattern 3](https://www.haoranma.info/vision.github.io/assets/images/pattern3_3.JPG)


### 3.4 Shape Pattern
After we activate the fourth pattern -- shape pattern. It shows the a complex colorful pattern designed by us using less than 10 lines of code. The visual effects are shown below:


<center>Shape Pattern 1</center>| <center>Shape Pattern 2</center>
--- | ---
![Shape Pattern 1](https://www.haoranma.info/vision.github.io/assets/images/pattern5_1.jpg) | ![Shape Pattern 2](https://www.haoranma.info/vision.github.io/assets/images/pattern5_2.JPG)


### 3.5 Text Pattern
After we input the text we want to show into the text box and submit it, it activates the last pattern -- text pattern. It shows the texts specified by us. Example visual effects are shown below (we use "hello" as an example):

<center>
<figure>
<figcaption align = "center"><b>Text Pattern</b></figcaption>
<img align="center" src="https://www.haoranma.info/vision.github.io/assets/images/pattern4.jpg" alt="Text Pattern" width="500"/>
</figure>
</center>