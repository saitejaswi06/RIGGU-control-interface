# 🤖 RIGGU Control Interface | RIG Induction Project

---

## 📌 Objectives

- Develop **ROS 2 nodes in Python** to control Riggu’s differential-drive base.
- Implement a **sound-based head rotation mechanism** to align the robot's head towards the source of sound.
- Design and implement a **battery management system (BMS)** for safe and efficient power handling.

---

## 🔑 Key Takeaways

- Learned fundamental working of **ESP8266-12E**, Arduino Uno, and their interfacing with motor drivers.
- Simulated circuits in **TinkerCAD**, **Wokwi**, and **Proteus** for prototyping the BMS.
- Built an RC car using ESP8266-12E and L293D to control dual motors via:
  - Serial communication (w/a/s/d on Arduino serial monitor).
  - WiFi-based control using an HTML server with keyboard arrow keys.
- Understood motor driver (L293D) control logic and PWM signal generation.
- Configured dual-boot system with **Pop!_OS** for working on ROS 2 Humble and Gazebo simulations.
- Explored **boost converters, buck converters**, and their voltage regulation role in Riggu.
- Learned the structure and behavior of **LiPo batteries**, including safe operating conditions.
- Explored **Lidar sensor** working principles and its navigation application in Riggu.
- Analyzed algorithms for **sound source localization** to control Riggu's head rotation.
- Initiated the **CAD design** for the rotating mechanism and learned basic mechanical integration.

---

## 🔋 Electronics | Battery Management System (BMS)

### Primary Components:
- **ATmega32 microcontroller** for core control.
- Voltage & current sensors to monitor battery status.
- Relay board for protective disconnection during fault conditions.

### Battery Monitoring:
- Continuously tracks voltage and discharge current.
- Automatically disconnects the load if:
  - Voltage drops below a safe threshold.
  - Current exceeds safe operating limits.

### Variable Voltage Source:
- Designed using **LM317 voltage regulator** and potentiometers for adjustable output.

### Safety Features:
- Relay control logic ensures safe voltage operation.
- Measured values are continuously logged and evaluated for system safety.

---

## 🔧 Mechanical | Rotating Head Mechanism

- CAD model features an acrylic **base mounting plate** with a center hole for servo coupling.
- **MG 996 Servo motor** securely mounted with brackets.
- A circular **servo head and shaft coupling** forms the neck assembly.
- Bearings and mechanical clearances ensure **smooth rotation** with minimal friction.

---

## 🕹️ ROS2-Based Joystick Control

### System Architecture:
- **driver_node (ROS2, Python):**
  - Subscribes to `/joy` topic from `joy_node`.
  - Converts joystick axes (linear + angular velocity) to left and right PWM control efforts.
  - Publishes PWM values to `/left_wheel/control_effort` and `/right_wheel/control_effort`.

- **connector_node (ESP32, C++ with micro-ROS):**
  - Subscribes to PWM topics.
  - Controls motor speeds via Cytron motor driver using GPIO PWM and direction pins.

### Communication:
- Micro-ROS agent runs in Docker, enabling **ROS 2-to-ESP32 communication**.

### Hardware Configuration:
| Component        | Pin Mapping |
|------------------|-------------|
| Left Motor PWM   | GPIO 18     |
| Left Motor DIR   | GPIO 19     |
| Right Motor PWM  | GPIO 21     |
| Right Motor DIR  | GPIO 22     |

### Validation:
- Used `rqt_graph` to verify ROS 2 node interactions.
- Tested robot’s response to joystick inputs for smooth differential drive control.

---

## 🛡️ Conclusion

This project provided hands-on learning in embedded systems, robotics control, and sensor integration. Key learnings include:
- **Balancing power management and mechanical load** for optimal battery life and safe operation.
- Designing robust mechanisms like the **servo-based head rotation**, minimizing mechanical strain and improving lifespan.
- Understanding the synergy between hardware design (power circuits, motors) and software (ROS2 nodes, microcontroller control).

The system architecture and practical implementations laid the groundwork for more advanced robotic solutions in sound-reactive navigation, autonomous mobility, and safe embedded system design.

---
