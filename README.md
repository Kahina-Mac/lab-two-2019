# Lab 2 Introduction to communication 
> It is mandetory to prepare your documents in `Markdown` format. We prepared an example repository in [Lab Report Sample](https://github.com/efrei-paris-sud/2019-sample-project/tree/master/lab/1). 
> All needed codes described in this repository. For more details about markdown please visit the [Example Report](https://github.com/efrei-paris-sud/2019-sample-project/tree/master/lab/1/report/1)

Put all reports into `lab/2/` folder in your repository. 
> Report Deadline = 15/11/2019
## Fritzing
The software is created in the spirit of the Processing programming language and the Arduino microcontroller[4] and allows a designer, artist, researcher, or hobbyist to document their Arduino-based prototype and create a PCB layout for manufacturing. 

- [Download Fritzing](https://github.com/fritzing/fritzing-app/releases/tag/CD-268)
- Create a new `sketch`.
- Search for `NodeMCU-32S` fritzing part and add it to Fritzing.
Note: please insure that the pin maps of the part is as same as the image in Lab 1.
- Create a random sketch your self (at least 5 component is needed and please don't forget connect them and use different colors in wiring)
-- Export the result as image(`lab/2/report/1/sketch.png`)
- Design the Schematic of that. Please style it in a good format.
-- Export the result as image(`lab/2/report/1/schematic.png`)
- Make a (`lab/2/report/1/README.md`) file and put a the images and a small description on it and **USE MARKDOWN FORMAT PLEASE**. For images please use the uploaded images from your `github`.
[Example Report](https://github.com/efrei-paris-sud/2019-sample-project/tree/master/lab/1/report/1)

# Communication 
In this lab, we will learn how the I2C/SPI/Serial communication protocol works.
## Serial 
The Wiring Serial serial port allows for easily reading and writing data to and from external devices. It allows two machines to communicate and gives you the flexibility to make your own devices and use them as the input or output to your Wiring programs.

The serial communication is very good for debuging your code. You can connect your arduino board to your computer easily. It works like a simple console. Let's start to use it.

In the Setup function we should define the Serial comunication. 
```C
void setup() {
  Serial.begin(9600);  // Start serial Serial at 9600 baud
}
```
> It is important that both devices have the same baud rate (transmission speed). [more info](https://fr.wikipedia.org/wiki/UART)
> You should change the baud rate in your client to read the data correctly.

To send data to the other device we can easily use. It will print `string`.
```C
Serial.print("string");
```
To read data from other device, we can use following code.
```C
byte b = Serial.read();
```
For more information click [here](http://wiring.org.co/reference/Serial.html)

A simple program:
```C
void setup() {
  // initialize serial:
  Serial.begin(9600);
  ....
}

void loop() {
  // if there's any serial available, read it:
  while (Serial.available() > 0) {

    // look for the next valid integer in the incoming serial stream:
    int i  = Serial.parseInt();
    // look for the next valid byte in the incoming serial stream:
    byte b = Serial.read();
    // look for the newline. That's the end of your sentence:
    if (Serial.read() == '\n') 
      .....
      
    // print the three numbers in one string as hexadecimal:
    Serial.print(15, HEX);//print F
    Serial.print(10, DEC);//Print 10
    Serial.println("Hello"); //Print Hello\n
    
  }
}
```

You can also connect 2 devices with serial communication. Please don't forget to connect TX from one side to RX in another side.

![serial communication](https://cdn.sparkfun.com/assets/2/5/c/4/5/50e1ce8bce395fb62b000000.png)

### Practic 2:
- Develop an arduino program which can read a byte from serial  and adjust the passive buzzer frequency with that. Write a response that your buzzer frequency changed to the read value. (`lab/2/report/2/code1.ino`).
- Follow the [following](https://highvoltages.co/tutorial/arduino-tutorial/arduino-real-time-plotting-with-python/) to plot the value read from variable resistor connected to A0 (`lab/2/report/2/code2.ino`).
- Create a Fritzing sketch contains both and export it on(`lab/2/report/2/sketch.png`).
- Connect your Arduino board to computer. Open a serial communication software (You can use built in serial monitor in Arduino IDE by pressing `ctrl`+`shift`+`M` or any other softwares like [Putty](https://www.putty.org/))
- Write a short report on (lab/2/report/2/README.md)

## I2C
I2C is a serial protocol for two-wire interface to connect low-speed devices.

Each device has a preset ID or a unique device address so the master can choose with which devices will be communicating. So many devices can communicate together with only 2 wires!

The two wires, or lines are called Serial Clock (or SCL) and Serial Data (or SDA).  The SCL line is the clock signal which synchronize the data transfer between the devices on the I2C bus and it’s generated by the master device. The other line is the SDA line which carries the data.

![I2C](https://www.analog.com/-/media/analog/en/landing-pages/technical-articles/i2c-primer-what-is-i2c-part-1-/36684.png?la=en&w=900)

The two lines are “open-drain” which means that pull up resistors needs to be attached to them so that the lines are high because the devices on the I2C bus are active low. Commonly used values for the resistors are from 2K for higher speeds at about 400 kbps, to 10K for lower speed at about 100 kbps. [More info on I2C](https://howtomechatronics.com/tutorials/arduino/how-i2c-communication-works-and-how-to-use-it-with-arduino/)

> BME 280 
> The GY-BME280 is a high precision combined digital pressure, humidity and temperature sensor module with I2C and SPI interfaces.
> ![BME 280](https://protosupplies.com/wp-content/uploads/2019/02/GY-BME280-Humidity-Pressure-Temperature-Sensor-Module-Connections.jpg)


Connect your arduino to bme280 using following sketch.
- VCC -> 5V
- GNF -> GND
- SCL -> A5
- SDA -> A4
![connect](http://static.cactus.io/img/hookups/arduino/connect-arduino-to-bme280-i2c-sensor.jpg)

To add BMP280 Library goto `Tools` -> `Library Manager` -> search for `BMP280`
### Part 3.1
Please use the example from [BMP280 Example](https://github.com/adafruit/Adafruit_BMP280_Library/tree/master/examples/bmp280test).
- Upload the code on(`lab/2/report/3/code1.ino`).
- Create a Fritzing sketch and export it on (`lab/2/report/3/sketch1.png`).
- Take a photo from your board (`lab/2/report/3/photo1.png`).
- Write a short report on (`lab/2/report/3/README.md`)

### Part 3.2
Connect your arduino to ESP32 using I2C.

Arduino|	ESP32
-|-
SDA (A4)	|SDA (default is GPIO 21)
SCL	(A5)  |SCL (default is GPIO 22)
GND	| GND 
VCC	| usually 3.3V or 5V (not needed if you are connected by usb)

- Create a Fritzing sketch and export it on (`lab/2/report/3/sketch2.png`).
- Upload the code on(`lab/2/report/3/arduino2.ino`, `lab/2/report/3/esp2.ino`).
- Take a photo from your board (`lab/2/report/3/photo2.png`).
- Write a short report on what is the following codes will do (`lab/2/report/3/README.md`) don't forget to include images in README.md

> Note: ESP32 has no slave mode.

Code for ESP32 for being in Master mode.
```C
#include <Wire.h>
// Include the required Wire library for I2C<br>#include 
int x = 0;
void setup() {
  // Start the I2C Bus as Master
  Wire.begin(); 
}
void loop() {
  Wire.beginTransmission(9); // transmit to device #9
  Wire.write(x);              // sends x 
  Wire.endTransmission();    // stop transmitting
  x++; // Increment x
  if (x > 5) x = 0; // `reset x once it gets 6
  delay(500);
}
```
Code For Slave (Arduino)
```C
#include <Wire.h>

// Include the required Wire library for I2C<br>#include <Wire.h>
int LED = LED_BUILTIN;
int x = 0;
void setup() {
  // Define the LED pin as Output
  Serial.begin(9600);
  pinMode (LED, OUTPUT);
  // Start the I2C Bus as Slave on address 9
  Wire.begin(9);
  Serial.println("Ok"); 
  
  // Attach a function to trigger when something is received.
  Wire.onReceive(receiveEvent);
}
void receiveEvent(int bytes) {
  x = Wire.read();    // read one character from the I2C
  Serial.println(x); 
}
void loop() {
  //If value received is 0 blink LED for 200 ms
  if (x == 0) {
    digitalWrite(LED, HIGH);
    delay(200);
    digitalWrite(LED, LOW);
    delay(200);
  }
  //If value received is 3 blink LED for 400 ms
  if (x == 3) {
    digitalWrite(LED, HIGH);
    delay(400);
    digitalWrite(LED, LOW);
    delay(400);
  }
}
```
### Part 3.3 (Bonus-Optional)
Ask me for GY-521 module.
This module has the MPU6050 which contains both a 3-Axis Gyroscope and a 3-Axis accelerometer allowing measurements of both independently, but all based around the same axes, thus eliminating the problems of cross-axis errors when using separate devices.
Connect your arduino to MPU6050 using following sketch.
- VCC -> 5V
- GNF -> GND
- SCL -> A5
- SDA -> A4

![MPU6050](mpu6050.png)

To add MPU6050 Library goto `Tools` -> `Library Manager` -> search for `MPU6050`

Look for Example added in File->Examples-> MPU6050 -> plotter

Upload it to arduino and see result in Serial.



  
## Report Deadline = 15/11/2019
## Exercise 1 (I2C) Deadline = 21/11/2019
- Connect ESP32, Arduino and BMP280 using I2C
- (Bonus-Optional) add MPU6050.
- Set Arduino as Slave with i2c address = 12 
- In Arudino write a code to :
  - Read input analog from A0 which is connected to a variable resistor. (Hint Practice 2)
  - Send the value to ESP32 using I2C

- Set ESP32 as Master
- In ESP32 write a code to: 
  - Read data from BMP280 
  - Read Value from Arduino (Read one byte)
  - (Bonus-Optional) Read data from MPU6050
  - Write values to the serial in comma seperated form.
  > Example: ```
  Index, Temperature,Pressure,Humidity, arduino input, acceleration.x,acceleration.y,acceleration.z, gyro.x, gyro.y, gyro.z
  
  ```
- Plot data in spreadsheet. (Copy all data in Serial Console to Excel and plot using that)
- Plot data in realtime Using (hint: review practice 2)
  
- Create a Fritzing sketch and export it on (`lab/2/exercise/1/sketch.png`).
- Upload the code on(`lab/2/exercise/1/arduino.ino`, `lab/2/exercise/1/esp.ino`).
- Take a photo from your board (`lab/2/exercise/1/photo.png`).
- Write a short report on how it works in (`lab/2/exercise/1/README.md`) don't forget to include images in README.md.



## Exercise 2 (SPI) Deadline = 22/11/2019 
SPI (Serial Peripheral Interface) is a serial communication protocol. SPI interface was found by Motorola in 1970. SPI has a full duplex connection, which means that the data is sent and received simultaneously. That is a master can send data to slave and a slave can send data to master simultaneously. SPI is synchronous serial communication means the clock is required for communication purpose.

SPI has following four lines MISO, MOSI, SS, and CLK

- MISO (Master in Slave Out) or SDO (Slave Data Out)- The Slave line for sending data to the master.
- MOSI (Master Out Slave In) or SDI (Slave Data In) - The Master line for sending data to the peripherals.
- SCK (Serial Clock) - The clock pulses which synchronize data transmission generated by the master.
- SS (Slave Select) – Master can use this pin to enable and disable specific devices.
 
![SPI](https://circuitdigest.com/sites/default/files/inlineimages/u/SPI-communication.png)

To start communication between master and slave we need to set the required device's Slave Select (SS) pin to LOW, so that it can communicate with the master. When it's high, it ignores the master. This allows you to have multiple SPI devices sharing the same MISO, MOSI, and CLK lines of master. 


Connect the BMP280 to **ESP32** via SPI. [More Info](http://cactus.io/hookups/sensors/barometric/bme280/hookup-arduino-to-bme280-barometric-pressure-sensor-spi)
- Don't fotget to use ESP32
- Find `MISO` `MOSI` `SCK` `SSS` in the pin maps from Lab 1 Readme file for ESP32.
- Create a Fritzing sketch and export it on (`lab/2/exercise/2/sketch.png`).
- Upload the code on(`lab/2/exercise/2/esp.ino`).
- Take a photo from your board (`lab/2/exercise/2/photo.png`).
- Write a short report on how it works in (`lab/2/exercise/2/README.md`) don't forget to include images in README.md.
- Enumare the differences between SPI and I2C in the README.md.
