# 🤖 Autonomous Obstacle Avoidance Robot

An Arduino Uno based autonomous robot that detects obstacles using ultrasonic sensors and automatically changes its direction to avoid collisions.

## 📌 Project Overview

The objective of this project is to develop a simple autonomous mobile robot capable of sensing obstacles in its surroundings and making movement decisions without manual control.

The robot continuously measures the distance in front, left and right directions using three HC-SR04 ultrasonic sensors. Based on the sensor readings, the Arduino Uno decides whether the robot should move forward, turn left, turn right, or reverse.

## 🛠️ Components Used

* Arduino Uno
* 3 × HC-SR04 Ultrasonic Sensors
* L293D Motor Driver
* 2 × DC Motors
* 3 Wheels

  * 2 powered wheels
  * 1 passive caster/support wheel
* 9V Battery / Power Supply
* Breadboard
* Connecting Wires

## ⚙️ System Architecture

```text
              HC-SR04 Sensors
          ┌──────┬──────┬──────┐
          │Front │ Left │Right │
          └──────┴───┬──┴──────┘
                     ↓
               ┌───────────┐
               │ Arduino   │
               │   Uno     │
               └─────┬─────┘
                     ↓
               ┌───────────┐
               │  L293D    │
               │Motor Driver│
               └─────┬─────┘
                     ↓
              ┌─────────────┐
              │ DC Motors   │
              │ Left + Right│
              └─────────────┘
                     ↓
                Robot Motion
                     ↓
              Sensors read again
```

## 🔄 Working Principle

The robot follows a simple sensor-based decision-making process:

1. The front HC-SR04 measures the distance to obstacles.
2. If the front distance is **≥ 20 cm**, the robot moves forward.
3. If the front distance is **< 20 cm**, the robot stops.
4. The left and right ultrasonic sensors then measure the available space.
5. If only the left side is clear, the robot turns left.
6. If only the right side is clear, the robot turns right.
7. If both sides are clear, the robot compares the distances and chooses the side with greater clearance.
8. If both sides are blocked, the robot reverses and reassesses the surroundings.
9. The process continuously repeats.

### Decision Logic

| Condition                  | Action                            |
| -------------------------- | --------------------------------- |
| Front ≥ 20 cm              | Move Forward                      |
| Front < 20 cm, Left clear  | Turn Left                         |
| Front < 20 cm, Right clear | Turn Right                        |
| Left & Right clear         | Choose side with greater distance |
| Left & Right blocked       | Reverse and reassess              |

## 🚗 Differential Drive

The robot uses a **differential-drive mechanism**.

The two DC motors are independently controlled:

| Left Motor | Right Motor | Movement   |
| ---------- | ----------- | ---------- |
| Forward    | Forward     | Forward    |
| Backward   | Backward    | Reverse    |
| Backward   | Forward     | Turn Left  |
| Forward    | Backward    | Turn Right |
| Stop       | Stop        | Stop       |

A third wheel is used as a **passive caster** to support and balance the robot. It is not motor-driven.

## 🔌 Pin Configuration

### L293D Motor Driver

| L293D Function | Arduino Pin |
| -------------- | ----------- |
| EN1            | D5          |
| IN1            | D7          |
| IN2            | D8          |
| EN2            | D6          |
| IN3            | D4          |
| IN4            | D3          |

### Ultrasonic Sensors

| Sensor | TRIG | ECHO |
| ------ | ---- | ---- |
| Front  | D9   | D10  |
| Left   | D11  | D12  |
| Right  | D13  | A0   |

> Note: A0 is used as a digital input for the right sensor's ECHO signal.

## 🧠 Control Logic

The core control loop can be summarized as:

```text
Sense
  ↓
Measure distances
  ↓
Check front obstacle
  ↓
Decide direction
  ↓
Control motors
  ↓
Move
  ↓
Sense again
```

The system uses **rule-based decision making** rather than machine learning or AI.

## 💡 Why Three Ultrasonic Sensors?

A single front-facing sensor can detect an obstacle but cannot determine which direction provides better clearance.

Using three sensors allows the robot to:

* Detect obstacles ahead
* Check the left path
* Check the right path
* Compare available space
* Make a direction decision

## 🔧 Role of L293D

The Arduino Uno is responsible for generating the motor-control signals, but its GPIO pins are not designed to directly drive DC motors.

The L293D acts as the motor-driver interface between the Arduino and the motors, allowing the Arduino to control motor direction and speed.

## 🧪 Testing

The project was developed and tested using a simulated Arduino-based circuit.

Testing included:

* Ultrasonic sensor distance measurement
* Forward motor movement
* Reverse motor movement
* Left and right turning
* Obstacle-detection logic
* Left/right path comparison

The circuit diagram and source code are included in this repository.

## ⚠️ Limitations

The current implementation uses a reactive, rule-based navigation approach. It makes decisions using the current sensor readings rather than creating a map of the environment.

Possible issues include:

* Ultrasonic sensor measurement noise
* Unequal motor speeds
* Difficulty in very narrow spaces
* Fixed distance threshold
* No wheel encoder feedback
* No mapping or localization

## 🚀 Future Improvements

The system could be improved by adding:

* Wheel encoders for accurate movement measurement
* PID-based motor speed control
* Sensor filtering and calibration
* Dynamic obstacle thresholds
* Better turning control
* Servo-mounted ultrasonic sensor
* Obstacle mapping
* Path-planning algorithms
* Localization and navigation

## 📂 Repository Contents

```text
Obstacle-Avoidance-Robot/
│
├── README.md
├── Arduino_Code/
│   └── obstacle_avoidance.ino
│
├── Circuit_Diagram/
│   └── circuit_diagram.png
│
└── Images/
    └── project_setup.png
```

## 🎯 Key Concepts Demonstrated

* Embedded Systems
* Arduino Programming
* Ultrasonic Distance Sensing
* GPIO Interfacing
* Motor Driver Interfacing
* PWM
* Differential Drive
* Sensor-Based Decision Making
* Real-Time Control
* Autonomous Navigation

## 👨‍💻 Project Summary

This project demonstrates how an embedded controller can combine multiple sensor inputs with actuator control to create a basic autonomous navigation system.

The main control principle is:

**Sense → Decide → Actuate → Repeat**

---

### 📄 Project Files

The repository contains the Arduino source code and circuit diagram used for the project.
