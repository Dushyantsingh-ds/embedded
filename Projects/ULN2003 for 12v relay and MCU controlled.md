## Wiring
![ Circuit ](https://github.com/Dushyantsingh-ds/embedded/blob/main/Projects/Assets/Schematic_ULN2003%20for%2012v%20relay%20and%20MCU%20controlled_2022-10-30.png)
[Download PDF](https://github.com/Dushyantsingh-ds/embedded/blob/main/Projects/Assets/Schematic_ULN2003%20for%2012v%20relay%20and%20MCU%20controlled_2022-10-30.pdf)

## Code 
```

// the setup function runs once when you press reset or power the board
void setup() {
  // initialize digital pin LED_BUILTIN as an output.
  pinMode(A0, OUTPUT);
  pinMode(A1, OUTPUT);
}

// the loop function runs over and over again forever
void loop() {
  digitalWrite(A0, HIGH);  
  delay(1000);     
  digitalWrite(A1, HIGH);  
  delay(1000);     
  digitalWrite(A0, LOW);    
  delay(1000);       
  digitalWrite(A1, LOW);    
  delay(1000);                       
}
```

## Wiring
![ Circuit ](https://github.com/Dushyantsingh-ds/embedded/blob/main/Projects/Assets/ULN2003%20for%2012v%20relay%20and%20MCU%20controlled.jpeg)

