# Autonomous Robot: Obstacle Avoidance + Black Target Navigation (Arduino)

This project is a 2-wheel differential drive robot built with **Arduino UNO**.  
It **avoids obstacles** using an **HC-SR04 ultrasonic sensor** and **navigates on a white floor to a black target area** using **two reflectance (line) sensors**.  
After reaching the target (both sensors detect black), the robot **replays its logged motion in reverse** to return to the start point.

## Demo / Hardware Photos
![Front view](images/robot-front.jpg)
![Top view](images/robot-top.jpg)
![Bottom view](images/robot-bottom.jpg)

## Key Features
- **Obstacle avoidance** with distance threshold (HC-SR04)
- **Black target detection** on white floor (dual analog sensors)
- **Finite state machine**: SEARCH → APPROACH → TARGET_FOUND → RETURNING → DONE
- **Motion logging**: saves motor commands and durations, then **reverses them** for return-to-start

## Hardware
- Arduino UNO
- L298N motor driver (2 DC gear motors)
- HC-SR04 ultrasonic sensor
- 2x reflectance / line sensors (analog)
- Battery pack + robot chassis

## Pin Mapping (from the code)
### Motor driver (L298N)
- ENA = 5, ENB = 6
- IN1 = 7, IN2 = 8, IN3 = 9, IN4 = 10

### Line / black sensors (analog)
- Left sensor  = A1
- Right sensor = A0

### HC-SR04
- TRIG = 12
- ECHO = 11

## How it works (Algorithm)
1. **SEARCH:** robot moves forward with a gentle left-right oscillation to scan the area.
2. **APPROACH:** if one sensor sees black, it steers to center the black region.
3. **TARGET_FOUND:** when both sensors detect black, it stops and finalizes the motion log.
4. **RETURNING:** it replays the recorded motor segments **in reverse** (negated PWM) to return.
5. **Obstacle priority:** if an obstacle is closer than the threshold, it performs an avoidance maneuver (also logged).

## Running the Code
1. Open `src/siyah_nokta_gidis_donus_engeleden_kacma.ino` in Arduino IDE
2. Select board: **Arduino Uno**
3. Select the correct COM port
4. Upload

## Calibration Notes
- `THRESH_BLACK` sets the black detection threshold (default: 600).  
  Adjust based on your sensors and surface.
- `OBSTACLE_CM` sets obstacle distance (default: 18 cm).
- `baseSpeed / turnSpeed` can be tuned for smoother approach.
