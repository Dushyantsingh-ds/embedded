Download library: [My Git LINK](https://github.com/Dushyantsingh-ds/embedded/blob/main/Projects/Assets/PCF8574_library-master.zip)) <br>
First finding the device Address by using the [My Git LINK](https://github.com/Dushyantsingh-ds/embedded/blob/main/Projects/Finding%20I2C%20connected%20devices%20with%20Ardunio.md) this code.

Code
```
#include "PCF8574.h"

// For arduino uno only pin 1 and 2 are interrupted
#define ARDUINO_UNO_INTERRUPTED_PIN 21

// Function interrupt
void keyPressedOnPCF8574();

// Set i2c address
PCF8574 pcf8574(0x20, ARDUINO_UNO_INTERRUPTED_PIN, keyPressedOnPCF8574);
unsigned long timeElapsed;
void setup()
{
	Serial.begin(115200);

	pcf8574.pinMode(P0, INPUT_PULLUP);
	pcf8574.pinMode(P1, INPUT_PULLUP);
	pcf8574.pinMode(P2, INPUT);
	pcf8574.pinMode(P3, INPUT);

	pcf8574.pinMode(P7, OUTPUT);
	pcf8574.pinMode(P6, OUTPUT, HIGH);
	pcf8574.pinMode(P5, OUTPUT);
	pcf8574.pinMode(P4, OUTPUT, LOW);

	Serial.print("Init pcf8574...");
	if (pcf8574.begin()){
		Serial.println("OK");
	}else{
		Serial.println("KO");
	}

	timeElapsed = millis();
}
unsigned long lastSendTime = 0;        // last send time
unsigned long interval = 4000;          // interval between sends

bool startVal = HIGH;

bool keyPressed = false;
void loop()
{
	if (keyPressed){
		uint8_t val0 = pcf8574.digitalRead(P0);
		uint8_t val1 = pcf8574.digitalRead(P1);
		uint8_t val2 = pcf8574.digitalRead(P2);
		uint8_t val3 = pcf8574.digitalRead(P3);
		Serial.print("P0 ");
		Serial.print(val0);
		Serial.print(" P1 ");
		Serial.print(val1);
		Serial.print(" P2 ");
		Serial.print(val2);
		Serial.print(" P3 ");
		Serial.println(val3);
		keyPressed= false;
	}

	  if (millis() - lastSendTime > interval) {
			pcf8574.digitalWrite(P7, startVal);
			if (startVal==HIGH) {
				startVal = LOW;
			}else{
				startVal = HIGH;
			}
			lastSendTime = millis();

			Serial.print("P7 ");
			Serial.println(startVal);
	  }
}

void keyPressedOnPCF8574(){
	// Interrupt called (No Serial no read no wire in this function, and DEBUG disabled on PCF library)
	 keyPressed = true;

}
```

Output wihout pressing any button
```
Init pcf8574...OK
P0 1 P1 1 P2 0 P3 0
P7 0
P0 1 P1 1 P2 1 P3 1
P7 1
P0 1 P1 1 P2 1 P3 1
```

Output with pressing P1,P2 button with GND (P1+GND, P2+GND)
```
Init pcf8574...OK
P0 1 P1 1 P2 0 P3 0
P7 0
P0 1 P1 1 P2 1 P3 1
P7 1
P0 1 P1 0 P2 1 P3 1
P7 0
P0 1 P1 0 P2 1 P3 1
P7 1
P0 1 P1 1 P2 0 P3 1
P7 0
P0 1 P1 1 P2 1 P3 1
```


Wiring
![Photo](https://github.com/Dushyantsingh-ds/embedded/blob/main/Projects/Assets/i2c%20Keypad%20project.jpeg)

