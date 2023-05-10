'''#include <Stepper.h>

// Define the number of steps per revolution for the steppers
const int stepsPerRevolution = 200;

// Define the number of steps required for a 1mm movement in each direction
const int stepsPer1mm = 200 / 5; // 5mm per step

// Initialize the stepper motors with their respective pins
Stepper stepper1(stepsPerRevolution, 9, 10, 11, 12);
Stepper stepper2(stepsPerRevolution, 5, 6, 7, 8);

// Define a function to move the steppers to a new position
void moveTo(int x, int y) {
  // Calculate the number of steps required to move in each direction
  int stepsX = x * stepsPer1mm;
  int stepsY = y * stepsPer1mm;

  // Move the stepper motors to the new position
  stepper1.step(stepsX);
  stepper2.step(-stepsY);
}

// Define the setup function to initialize the stepper motors
void setup() {
  // Set the speed of the stepper motors
  stepper1.setSpeed(60);
  stepper2.setSpeed(60);

  // Set the initial position to (0, 0)
  moveTo(0, 0);
}

// Define the main loop function to process G-code commands
void loop() {
  // Read a G-code command from Serial
  
  String cmd[3] = {"G1 X5 Y0\n","G1 X0 Y5\n","G1 X1 Y1\n"}; // replace this with your code input string
for(int i =0;i<=3;i++){
  // Parse the X and Y values from the command
  int xPos = 0;
  int yPos = 0;
  int cmdLength = cmd[i].length();
  int cmdIndex = 0;
  char currentChar = cmd[i].charAt(cmdIndex);
  while (cmdIndex < cmdLength) {
    if (currentChar == 'G') {
      // Ignore G-code commands other than G1
      cmdIndex += 2;
      currentChar = cmd[i].charAt(cmdIndex);
    } else if (currentChar == 'X') {
      // Parse the X value
      cmdIndex++;
      String xValStr = "";
      while (cmdIndex < cmdLength && isDigit(cmd[i].charAt(cmdIndex))) {
        xValStr += cmd[i].charAt(cmdIndex);
        cmdIndex++;
      }
      xPos = xValStr.toInt();
    } else if (currentChar == 'Y') {
      // Parse the Y value
      cmdIndex++;
      String yValStr = "";
      while (cmdIndex < cmdLength && isDigit(cmd[i].charAt(cmdIndex))) {
        yValStr += cmd[i].charAt(cmdIndex);
        cmdIndex++;
      }
      yPos = yValStr.toInt();
    } else {
      cmdIndex++;
    }
    currentChar = cmd[i].charAt(cmdIndex);
  }

  // Move the steppers to the new position
  moveTo(xPos, yPos);

  // Wait for the steppers to finish moving
  delay(1000);
}

}
'''
