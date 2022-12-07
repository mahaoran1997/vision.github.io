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
* 9cm &#xD7; 10cm PCB Board
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

We built a demo system and created five different patterns using our library to show its usability. Our demo system has a web interface, and users can select which pattern to show on our led display through buttons on the webpage. To open the webpage, users firstly need to connect to the wifi channel created by our system and goto 192.168.4.1 in your browser app. The page is shown below: 

![Example Web Page](https://www.haoranma.info/vision.github.io/assets/images/WebPage.PNG)

We can see five different patterns on the website. After we activate the first pattenr -- color pattern which is the simplest one in this demo. It changes its color every 5 seconds. The visual effects are shown below:
![Color Pattern 1](https://www.haoranma.info/vision.github.io/assets/images/pattern1_1.JPG)
![Color Pattern 2](https://www.haoranma.info/vision.github.io/assets/images/pattern1_2.JPG)


The web page looks 







