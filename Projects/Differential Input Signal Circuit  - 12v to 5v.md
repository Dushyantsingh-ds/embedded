## Wiring
![ Circuit ](https://github.com/Dushyantsingh-ds/embedded/blob/main/Projects/Assets/Schematic_differential%20Input%20Signal%20Circuit_2022-10-29.png)
[Download PDF](https://github.com/Dushyantsingh-ds/embedded/blob/main/Projects/Assets/Schematic_differential%20Input%20Signal%20Circuit_2022-10-29.pdf)

## Code 
```
const int buttonPin = A1;
const int ledPin =  13; 

int buttonState = 0;  

void setup() {
  Serial.begin(9600);
  pinMode(ledPin, OUTPUT);
  pinMode(buttonPin, INPUT);
}

void loop() {
  buttonState = digitalRead(buttonPin);

  if (buttonState == HIGH) {
    digitalWrite(ledPin, HIGH);
    Serial.println("HIGH");
  } else {
    digitalWrite(ledPin, LOW);
    Serial.println("LOW");
  }
}
```

## Wiring
![ Circuit ](https://github.com/Dushyantsingh-ds/embedded/blob/main/Projects/Assets/Schematic_differential%20Input%20Signal%20Circuit%20output.jpeg)

