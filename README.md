# Arduino obstacle-avoiding car

A small autonomous car built on an Arduino Uno and the Adafruit Motor Shield. It drives forward until an HC-SR04 ultrasonic sensor detects an obstacle, then stops, reverses, scans left and right with a servo-mounted sensor, and turns toward whichever side has more open space. Two indicator LEDs show what the car is currently doing.

## Demo behavior

- Drives forward when the path is clear
- Stops and reverses when an obstacle is within range
- Scans left and right using the servo to find the more open direction
- Turns toward the clearer side and resumes driving
- Right LED lights up on a right turn, left LED on a left turn, both LEDs on while driving forward, and both blink while reversing

## Parts list

| Part | Notes |
|---|---|
| Arduino Uno | Or compatible board |
| Adafruit Motor Shield (v1) | Stacks directly on top of the Uno |
| 4x DC gear motors | Connected to M1-M4 on the shield |
| HC-SR04 ultrasonic sensor | Obstacle detection |
| SG90 (or similar) servo | Sweeps the sensor left and right |
| 2x LEDs | Status indicators |
| 2x 220 ohm resistors | One per LED |
| 4x AA/AAA battery pack or 7.4V Li-ion pack | Powers the motor shield separately from the Uno |
| Chassis with 4 wheels | Any 4WD robot chassis kit |
| Jumper wires | |

## Wiring

### Core build

The Arduino Uno, motor shield, sensor, and servo:

![Core wiring diagram](images/wiring-core.svg)


### Pin reference

| Component | Arduino pin |
|---|---|
| HC-SR04 Trig | A1 |
| HC-SR04 Echo | A3 |
| Servo signal | 10 |
| Right LED (through resistor) | A0 |
| Left LED (through resistor) | A2 |
| Motors | M1-M4 on the motor shield |

**Power note:** the motor shield needs its own battery pack for the motors. Don't try to run the motors off the Uno's USB or barrel-jack power — it isn't enough current and can damage the board.

## Libraries required

This project needs three libraries. `Servo` ships with the Arduino IDE; the other two need manual installation since they aren't in the Library Manager.

| Library | Source | Install method |
|---|---|---|
| AFMotor | [Adafruit Motor Shield library](https://github.com/adafruit/Adafruit-Motor-Shield-library) | Download ZIP → Sketch → Include Library → Add .ZIP Library |
| NewPing | [Arduino-NewPing](https://github.com/livetronic/Arduino-NewPing) | Library Manager search, or ZIP install |
| Servo | Bundled with Arduino IDE | No install needed |

After installing AFMotor or NewPing via ZIP, **restart the Arduino IDE** before compiling.

## Setup

1. Install the libraries above.
2. Wire the components according to the diagrams and pin reference table.
3. Open `robot.ino` in the Arduino IDE.
4. Select your board and port under **Tools**.
5. Upload the sketch.
6. Power the motor shield from the battery pack, then power on.

## Tuning

A few constants in the sketch you may want to adjust for your build:

| Constant | Default | Effect |
|---|---|---|
| `MAX_SPEED` | 190 | Top motor speed (0-255) |
| `MAX_DISTANCE` | 200 | Max sensor range in cm |
| Obstacle threshold | 60 | Distance in cm that triggers avoidance, set in the `if(distance<=60)` check in `loop()` |

## Project Image

