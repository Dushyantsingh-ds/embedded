```#include <Stepper.h>

// Define the number of steps per revolution
const int STEPS_PER_REV = 320;

// Define the line length and step size
const int LINE_LENGTH = 15;
const int STEP_SIZE = 5;

// Define the stepper motor connections
Stepper stepper1(STEPS_PER_REV, 9, 10, 11, 12);
Stepper stepper2(STEPS_PER_REV, 5, 6, 7, 8);

// Define the penumatic solenoid connection
const int SOLENOID_PIN = 13;

void setup() {
  // Set the speed of the stepper motors
  stepper1.setSpeed(100);
  stepper2.setSpeed(100);

  // Set the penumatic solenoid pin to output mode
  pinMode(SOLENOID_PIN, OUTPUT);

  // Set the penumatic solenoid to its initial state (off)
  digitalWrite(SOLENOID_PIN, LOW);
}

void loop() {
  // Move to the starting position
  Gcode("G0 X20 Y20 Z10\n");

  // Lower the penumatic solenoid
  digitalWrite(SOLENOID_PIN, HIGH);

  // Draw the letter "Z"
  Gcode("G1 X70 Y20\n");
  
  Gcode("G1 X20 Y70\n");
  Gcode("G1 X70 Y70\n");
  Gcode("G1 X20 Y120\n");

  // Raise the penumatic solenoid
  digitalWrite(SOLENOID_PIN, LOW);

  // Move back to the starting position
  Gcode("G0 X20 Y20 Z10\n");

  // Wait for a moment before starting again
  delay(1000);
}

// Helper function to send G-code commands to the stepper motors
void Gcode(String command) {
  for (int i = 0; i < command.length(); i++) {
    switch (command[i]) {
      case 'X':
        moveX(command.substring(i + 1, command.indexOf(' ', i + 1)).toFloat());
        break;
      case 'Y':
        moveY(command.substring(i + 1, command.indexOf(' ', i + 1)).toFloat());
        break;
      case 'Z':
        moveZ(command.substring(i + 1, command.indexOf(' ', i + 1)).toFloat());
        break;
      case 'G':
        // Ignore the G-code command
        break;
      default:
        // Unknown command
        break;
    }
  }
}

// Helper function to move the stepper motors to a specific X position
void moveX(float x) {
  int steps = (int) ((x - LINE_LENGTH / 2) * STEPS_PER_REV / STEP_SIZE);
  stepper1.step(steps);
}

// Helper function to move the stepper motors to a specific Y position
void moveY(float y) {
  int steps = (int) ((y - LINE_LENGTH / 2) * STEPS_PER_REV / STEP_SIZE);
  stepper2.step(steps);
}

// Helper function to move the penumatic solenoid to a specific Z position
void moveZ(float z) {
  // Not implemented for this example
}
```
