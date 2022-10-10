# Boot Atmega328 with ISP to program

My pervious Post for [Bootloading : ](https://github.com/Dushyantsingh-ds/embedded/blob/main/Projects/Boot%20Atmega328%20with%20ISP%20to%20program%20ATmega328%20IC%20without%20a%20crystal.md) <br>
Reffrance : http://eng-shady-mohsen.blogspot.com/2018/03/programming-atmel-atmega328-pu.html

[1] Connect the following pins on ATMEGA328-PU microcontroller (target) to Arduino Mega board (which is used now as programmer):

|     Arduino Mega 2560 (programmer) Pin name      | ATMEGA328-PU (target) Pin name  |
| :--- |  :---: |  
| GND | GND       |
| VCC  | VCC       |
| D10 |RESET        |
| D51 (MOSI)  |D11        |
| D50 (MISO) | D12 |
| D52 (SCK)| D13  |

![pins](https://github.com/Dushyantsingh-ds/embedded/blob/main/Projects/Assets/bootloader%201.5.gif)

Programming Atmel ATMEGA328-PU microcontroller using Arduino Mega board <br>
The following method is used if ATMEGA328-PU microcontroller will be used with external oscillator 16 MHz. 

## A. Make the programmer

First: Software preparation:
[1] Before any wiring or creating any mess, connect Arduino Mega 2560 board to your PC using the USB cable

[2] Open Arduino IDE -> File -> Examples -> 11.Arduino ISP -> ArduinoISP.
By doing this "ArduinoISP" sketch will be opened. Keep the sketch as it is without any modification.

[3] Select Tools -> Board -> Arduino/Genuino Mega or Mega2560

[4] Select Tools -> Processor -> ATMEGA2560

[5] Select the correct COM port from Tools -> Port

[6] Select Sketch -> Upload

[7] By uploading the sketch, we have finished the software part.

Second: Hardware preparation:

[1] As many references said, we need 10 uF electrolytic capacitor (in my case I used a 33 uF capacitor which was available for me and it did the job). Connect the positive (long) lead of the capacitor to RESET pin of Arduino Mega 2560 and the short (negative) lead of the capacitor to GND pin of Arduino Mega. This capacitor is needed to disable resetting Arduino Mega.

[2] Now, we have turned our Arduino Mega 2560 to a programmer.


## B. Burn the boot loader on target microcontroller

[2] Open Arduino IDE. Now, we will use the settings of the target microcontroller board.

[3] Tools -> Board -> Arduino Duemilanove or Decimilia

[4] Tools -> Processor -> ATmega328

[5] Tools -> Programmer -> Arduino as ISP

[6] Tools -> Burn boot loader

[7] Now, you have successfully turned your virgin ATMEGA328-20PU microcontroller to an Arduino-compatible microcontroller. Keep the previous wire connections and don't remove them because we will use them in the next step.



## C. Upload your own sketch to your new microcontroller

[1] Create new sketch. I prefer using blinking LED sketch as a kick off

[2] Tools -> Board -> Arduino Duemilanove or Decimilia

[3] Tools -> Processor -> ATmega328

[4] Sketch -> Upload Using Programmer

[5] Congratulations. Your sketch is uploaded and your microcontroller is standalone.
