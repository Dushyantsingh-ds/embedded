# PWD based LED dimmer
![ Led Dimmer ](https://miro.medium.com/max/1026/1*2DPbu3Tl4Dh_GgppVOnXXQ.jpeg)

## Circuit Wirring
![ Led Dimmer ](https://miro.medium.com/max/610/1*O6sTKlokn1Lxthbug-ZnjA.png)
## Code 
Sketch for LED fading using Arduino PWM
```
int led = 3; // the PWM pin the LED is attached to
int brightness = 0; // how bright the LED is
int fadeAmount = 5; // how many points to fade the LED by
void setup() {
pinMode(led, OUTPUT); // declare pwm pin to be an output:
}
void loop() {
analogWrite(led, brightness); // set the brightness of led
// change the brightness for next time through the loop:
brightness = brightness + fadeAmount;
// reverse the direction of the fading at the ends of the fade:
if (brightness <= 0 || brightness >= 255) {
fadeAmount = -fadeAmount;
}
delay(30); // wait for 30 milliseconds to see the dimming effect }

```

### Connect with me:

[<img align="left" alt="Dushyant Singh | LinkedIn" width="22px" src="https://cdn.jsdelivr.net/npm/simple-icons@v3/icons/linkedin.svg" />][linkedin]
[<img align="left" alt="Dushyant Singh | Twitter" width="22px" src="https://cdn.jsdelivr.net/npm/simple-icons@v3/icons/twitter.svg" />][twitter]
[<img align="left" alt="Dushyant Singh | GitHub" width="22px" src="https://cdn.jsdelivr.net/npm/simple-icons@v3/icons/medium.svg" />][github]
[<img align="left" alt="Dushyant Singh | Medium" width="22px" src="https://raw.githubusercontent.com/iconic/open-iconic/master/svg/globe.svg" />][medium]
[<img align="left" alt="Dushyant Singh | Instagram" width="22px" src="https://cdn.jsdelivr.net/npm/simple-icons@v3/icons/instagram.svg" />][instagram]
[<img align="left" alt="Dushyant Singh | Facebook" width="22px" src="https://cdn.jsdelivr.net/npm/simple-icons@v3/icons/facebook.svg" />][facebook]
[<img align="left" alt="Dushyant Singh | Telegram" width="22px" src="https://cdn.jsdelivr.net/npm/simple-icons@v3/icons/telegram.svg" />][telegram]

<br />

[medium]: https://dushyantsingh-ds.medium.com/
[linkedin]: https://linkedin.com/in/dushyantsingh-ds/
[instagram]: https://www.instagram.com/dushyantsingh.ds/
[twitter]: https://twitter.com/dushyantsingh_d
[facebook]: https://www.facebook.com/dushyantsingh.india
[github]: https://github.com/Dushyantsingh-ds
[telegram]: https://t.me/dushyantsingh_d

 
