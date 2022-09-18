## Wiring
```

```
## Code 
```
int led = A1;  
int PinButton = A0;  
void setup()  
{  
    pinMode(PinButton, INPUT);  
    pinMode(led, OUTPUT);  
    Serial.begin(9600);
}  
void loop()  
{  
    int stateButton = digitalRead(PinButton);  
    if (stateButton == 1)  
    {  
       Serial.println('0');
       digitalWrite(led, HIGH); // Turn on led  
    }  
    else  
    {  
        digitalWrite(led, LOW); //Turn off led  
    }  
    delay(200);  
}  
```
