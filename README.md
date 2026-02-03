# Autonomous Robot: Obstacle Avoidance + Black Target Navigation (Arduino)

A 2-wheel differential drive robot built with **Arduino UNO** that:
1) **Avoids obstacles** using an **HC-SR04 ultrasonic sensor**
2) **Navigates on a white floor to a black target area** using **two reflectance (line) sensors**
3) **Logs motion steps** and **replays them in reverse** to return to the start point

## Hardware Photos
![Front view](images/robot-front.jpg)
![Top view](images/robot-top.jpg)
![Bottom view](images/robot-bottom.jpg)

## System Overview
**Controller:** Arduino UNO  
**Actuation:** 2x DC gear motors (differential drive) + L298N motor driver  
**Sensing:** HC-SR04 distance + 2x reflectance sensors (black/white detection)  
**Power:** Battery pack (chassis mounted)

## Core Behaviors (Algorithm)
- **Search / Cruise:** robot moves forward and scans
- **Obstacle Avoidance:** if distance < threshold → avoid maneuver (turn + continue)
- **Black Target Approach:** steering logic based on left/right sensor readings
- **Target Found:** when both sensors detect black → stop and mark success
- **Return to Start:** replay recorded motor commands **in reverse order** (reverse PWM)

## Code
- `siyah_nokta_gidis_donus_engeleden_kacma.ino` — main Arduino sketch

## Pin Mapping (as used in the code)
### Motor driver (L298N)
- ENA = 5, ENB = 6  
- IN1 = 7, IN2 = 8, IN3 = 9, IN4 = 10  

### Reflectance sensors (analog)
- Right sensor = A0  
- Left sensor  = A1  

### Ultrasonic sensor (HC-SR04)
- TRIG = 12  
- ECHO = 11  

## How to Run
1. Open the `.ino` file in **Arduino IDE**
2. Select Board: **Arduino Uno**
3. Select the correct COM port
4. Upload

## Tuning / Calibration
- `THRESH_BLACK` → adjust based on sensor + surface (black detection)
- `OBSTACLE_CM` → obstacle distance threshold
- `baseSpeed`, `turnSpeed` → smoother control and turning
