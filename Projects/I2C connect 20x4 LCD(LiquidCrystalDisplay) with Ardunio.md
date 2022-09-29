Download library: [My Git LINK](https://github.com/Dushyantsingh-ds/embedded/blob/main/Projects/Assets/Arduino-LiquidCrystal-I2C-library-master.zip) <br>
First finding the device Address by using the [My Git LINK](https://github.com/Dushyantsingh-ds/embedded/blob/main/Projects/Finding%20I2C%20connected%20devices%20with%20Ardunio.md) this code.

Code
```

#include <LiquidCrystal_I2C.h>

// Set the LCD address to 0x27 for a 16 chars and 2 line display
LiquidCrystal_I2C lcd(0x27, 20, 4);

void setup()
{
  // initialize the LCD
  lcd.begin();

  // Turn on the blacklight and print a message.
  lcd.backlight();
  //lcd.noBacklight();
    lcd.setCursor(2, 0);

  lcd.print("Truth Power Info.");
  
  lcd.setCursor(3, 1);
  lcd.print("Model: SM-V1.0");
  delay(1000);
   lcd.setCursor(1, 3);
  lcd.print("truthpowerinfo.com");
  
}

void loop()
{
  // Do nothing here...
}
```

output
![Photo](https://github.com/Dushyantsingh-ds/embedded/blob/main/Projects/Assets/i2c%20LCD%20project.jpeg)
