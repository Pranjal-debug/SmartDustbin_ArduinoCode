# Smart Autonomous Trash Bin

## Overview

This project is a **Smart Autonomous Trash Bin** built using Arduino, ultrasonic sensors, IR sensors, a servo motor, and an L298N motor driver.

The system operates in two modes:

1. **Normal Mode**

   * Detects a user's hand near the bin.
   * Automatically opens the lid using a servo motor.
   * Closes the lid after a few seconds.

2. **Full Bin Mode**

   * Detects when the trash level reaches a predefined threshold.
   * Closes the lid permanently.
   * Activates a line-following robot mechanism using IR sensors.
   * Moves the bin toward a designated disposal or collection point.

---

## Features

* Automatic touchless lid opening.
* Trash level monitoring using ultrasonic sensing.
* Automatic full-bin detection.
* Autonomous movement when the bin is full.
* Line-following navigation.
* Differential drive control using L298N motor driver.
* Servo-controlled lid mechanism.

---

## Hardware Requirements

### Microcontroller

* Arduino Uno / Nano

### Sensors

* 1 × Ultrasonic Sensor (Trash Level Detection)
* 1 × Ultrasonic Sensor (Hand Detection)
* 2 × IR Line Tracking Sensors

### Actuators

* 1 × Servo Motor (SG90 or similar)
* 2 × DC Gear Motors

### Motor Driver

* L298N Motor Driver Module

### Power Supply

* Battery Pack (appropriate for motors and Arduino)

---

## Pin Configuration

| Component        | Arduino Pin |
| ---------------- | ----------- |
| Left IR Sensor   | D2          |
| Right IR Sensor  | D3          |
| Motor A IN1      | D4          |
| Motor A IN2      | D5          |
| Servo Motor      | D6          |
| Fill Sensor TRIG | D7          |
| Fill Sensor ECHO | D8          |
| Hand Sensor TRIG | D9          |
| Hand Sensor ECHO | D10         |
| Motor B IN3      | D11         |
| Motor B IN4      | D12         |

---

## Working Principle

### 1. Normal Mode

The fill-level ultrasonic sensor continuously measures the distance between the sensor and the garbage.

If the measured distance is:

* Greater than 7 cm → Bin is considered available.
* Hand detected within 15 cm → Lid opens.

Process:

1. Hand approaches bin.
2. Hand sensor detects object.
3. Servo rotates to 90°.
4. Lid remains open for 3 seconds.
5. Servo returns to 0°.

---

### 2. Full Bin Detection

The fill-level ultrasonic sensor measures the distance from the top of the bin to the garbage.

Conditions:

* Distance ≤ 7 cm → Bin Full
* Distance ≥ 18 cm → Bin Empty Again

This hysteresis prevents rapid switching between states.

---

### 3. Autonomous Navigation

When the bin becomes full:

* Lid remains closed.
* IR sensors begin line tracking.
* Motors are activated.

Movement Logic:

| Left IR | Right IR | Action       |
| ------- | -------- | ------------ |
| 0       | 0        | Move Forward |
| 1       | 0        | Turn Left    |
| 0       | 1        | Turn Right   |
| 1       | 1        | Stop         |

---

## Motor Speed Control

Motor speed is controlled by pulse-based movement.

Variables:

```cpp
int motorOnTime = 25;
int motorOffTime = 10;
```

### Increase Speed

```cpp
motorOnTime = 40;
motorOffTime = 5;
```

### Decrease Speed

```cpp
motorOnTime = 15;
motorOffTime = 20;
```

---

## Serial Monitor Output

Example output:

```text
Hand: 8.5  Fill: 22.1
OPENING LID
```

Full mode:

```text
FULL MODE | L=0 R=0
```

---

## Applications

* Smart Homes
* Colleges and Universities
* Offices
* Hospitals
* Public Waste Collection Systems
* Smart City Projects

---

## Future Improvements

* Wi-Fi/IoT monitoring using ESP8266 or ESP32.
* Mobile app integration.
* Automatic charging station.
* GPS-based navigation.
* Multiple destination selection.
* Weight sensor integration.
* Waste segregation system.

---

## Authors

Developed as an Arduino-based Smart Autonomous Trash Bin project combining:

* Touchless waste disposal
* Fill-level monitoring
* Autonomous navigation
* Basic robotics and automation

This project demonstrates concepts from embedded systems, robotics, sensors, motor control, and smart waste management.
