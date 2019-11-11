# lab-two-2019
Put all reports into `Lab/2/` folder in your repository. 
## Fritzing
The software is created in the spirit of the Processing programming language and the Arduino microcontroller[4] and allows a designer, artist, researcher, or hobbyist to document their Arduino-based prototype and create a PCB layout for manufacturing. 

- [Download Fritzing](https://github.com/fritzing/fritzing-app/releases/tag/CD-268)
- Create a new `sketch`.
- Search for `NodeMCU-32S` fritzing part and add it to Fritzing.
Note: please insure that the pin maps of the part is as same as the image in Lab 1.
- Create the following sketch. (Instead of Char A in the Sketch use first letter of your group name)
-- Export the result as image(`Lab/2/Report/1/sketch.png`)
- Design the Schematic of that. Please style it in a good format.
-- Export the result as image(`Lab/2/Report/1/schematic.png`)
- Make a (`Lab/2/Report/1/README.md`) file and put a the images and a small description on it and **USE MARKDOWN FORMAT PLEASE**. For images please use the uploaded images from your `github`.
[Markdown-Cheatsheet](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet)

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
It is important that both devices have the same baud rate (transmission speed). [more info](https://fr.wikipedia.org/wiki/UART)

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
### Practic 2:
- Develop an arduino program which can read from serial and adjust the passive buzzer frequency.(`Lab/2/Report/2/code.ino`).
- Create a Fritzing sketch and export it on(`Lab/2/Report/2/sketch.png`).
- Connect your Arduino board to computer. Open a serial communication software(you can use built in serial monitor in Arduino IDE by pressing `ctrl`+`shift`+`M` or any other softwares like [Putty](https://www.putty.org/))
- Write a short report on (Lab/2/Report/2/README.md)

## I2C
Please follow the tutorial from [I2C](https://howtomechatronics.com/tutorials/arduino/how-i2c-communication-works-and-how-to-use-it-with-arduino/)
Use ... instead of GY-80.
- Upload the code on(`Lab/2/Report/3/code.ino`).
- Create a Fritzing sketch and export it on (`Lab/2/Report/3/sketch.png`).
- Take a photo from your board (`Lab/2/Report/3/photo.png`).
- Write a short report on (`Lab/2/Report/3/README.md`)


## SPI
Please follow the tutorial from  [SPI](https://circuits4you.com/2019/01/03/arduino-spi-communication-example/)

Instead using 2 Arduino Uno, We will use one Arduino Uno and one ESP32.
- Find `MISO` `MOSI` `` ``
- Upload the code on(`Lab/2/Report/4/arduino.ino`, `Lab/2/Report/4/esp32.ino`).
- Create a Fritzing sketch and export it on (`Lab/2/Report/4/sketch.png`).
- Take a photo from your board (`Lab/2/Report/4/photo.png`).
- Write a short report on (`Lab/2/Report/4/README.md`)


## SPI vs I2C
- I2C requires only two wires, while SPI requires three or four.
- SPI supports higher speed full-duplex communication while I2C is slower.
- I2C draws more power than SPI.
- I2C supports multiple devices on the same bus without additional select signal lines through in-communication device addressing while SPI requires additional signal lines to manage multiple devices on the same bus.
- I2C ensures that data sent is received by the slave device while SPI does not verify that data is received correctly.
- I2C can be locked up by one device that fails to release the communication bus.
- SPI cannot transmit off the PCB while I2C can, albeit at low data transmission speeds.
- I2C is cheaper to implement than the SPI communication protocol.
- SPI only supports one master device on the bus while I2C supports multiple master devices.
- I2C is less susceptible to noise than SPI.
- SPI can only travel short distances and rarely off of the PCB while I2C can transmit data over much greater distances, although at low data rates.
- The lack of a formal standard has resulted in several variations of the SPI protocol, variations which have been largely avoided with the I2C protocol.
