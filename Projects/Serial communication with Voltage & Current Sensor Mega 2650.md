
```
String IS , VS;
int DPos1, DPos2, CPos, VPos;
char solarByte;
String solar, solar2, solar3;
const byte D2 = 18;
const byte D1 = 19;

void setup()
{
  Serial.begin(9600);
  while (!Serial) {
    ;
  }
}

void loop()
{
  while (Serial.available()) {
    solarByte = Serial.read();
    solar.concat(solarByte);
  }
 Serial.println(solarByte);
  DPos1 = solar.indexOf('D');
  DPos2 = solar.indexOf('D', DPos1 + 1);
  CPos = solar.indexOf('C');
  VPos = solar.indexOf('V');
  IS = solar.substring(CPos+1, DPos1);
  VS = solar.substring(VPos + 1, DPos2);

  IS = "Current :" + IS;
  VS = "Voltage :" + VS;
  Serial.println(IS);
  Serial.println(VS);
  solar = "";
  delay(1000);
}
```
