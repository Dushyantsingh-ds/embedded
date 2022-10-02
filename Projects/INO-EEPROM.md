EEPROM is a memory whose values are kept when the board is powered off.

Reffrance: https://docs.arduino.cc/learn/built-in-libraries/eeprom

## Functions

### write()
<details>
  <summary>Click to expand!</summary>
  
Syntax:
  
  ``` 
  EEPROM.write(address, value)
  ```
  
  Example: 
  
  ```
#include <EEPROM.h>

void setup()
{
  Serial.begin(9600);
  int WriteVal_ = 24;
  
  Serial.println(WriteVal_);
  EEPROM.write(0, WriteVal_);
}

void loop()
{ 
  int ReadVal_ = EEPROM.read(0);
  Serial.println(ReadVal_);
}                          
  ```
</details> 
  
### read()
<details>
  <summary>Click to expand!</summary>
  
Syntax:
  
  ``` 
  EEPROM.read(address)
  ```
  
  Example: 
  
  ```
#include <EEPROM.h>

void setup()
{
  Serial.begin(9600);
}

void loop()
{ 
  int ReadVal_ = EEPROM.read(0);
  Serial.println(ReadVal_);
}                          
  ```
</details> 
  
  
### update()
<details>
<summary>Click to expand!</summary>
  
Syntax:
  
``` 
EEPROM.update(address, value)
 ```

Example: 
  
```
#include <EEPROM.h>

void setup()
{
  Serial.begin(9600);
}

void loop()
{ 
  int UpdateVal_ = 2026;
  EEPROM.update(0, UpdateVal_)
}                          
    
```
</details>
      
### get()
<details>
<summary>Click to expand!</summary>
  
Syntax:
  
``` 

```

Example: 
  
```
#include <EEPROM.h>

void setup()
{
  Serial.begin(9600);
}

void loop()
{ 
 //Code
}                          
    
```
</details>
    
### put()

<details>
<summary>Click to expand!</summary>
  
Syntax:
  
``` 

```

Example: 
  
```
#include <EEPROM.h>

void setup()
{
  Serial.begin(9600);
}

void loop()
{ 
 //Code
}                          
    
```
</details>
  
      
### EEPROM[]
<details>
<summary>Click to expand!</summary>
  
Syntax:
  
``` 

```

Example: 
  
```
#include <EEPROM.h>

void setup()
{
  Serial.begin(9600);
}

void loop()
{ 
 //Code
}                          
    
```
</details>
        
### length()
<details>
<summary>Click to expand!</summary>
  
Syntax:
  
``` 

```

Example: 
  
```
#include <EEPROM.h>

void setup()
{
  Serial.begin(9600);
}

void loop()
{ 
 //Code
}                          
    
```
</details>
  
  
  
