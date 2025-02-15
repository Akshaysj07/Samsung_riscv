# Ultrasonic Obstacle Detection using VSDSquadron Mini

## Overview
This project implements an **ultrasonic obstacle detection system** using an **HC-SR04 ultrasonic sensor** and an **active buzzer** on the **VSDSquadron Mini Board**. The system detects obstacles and provides **audible alerts** based on distance.

---


## 1. Working Principle
1. The **HC-SR04 ultrasonic sensor** sends ultrasonic pulses.
2. The **time taken for the echo to return** is measured.
3. The **distance of an obstacle** is calculated using the time delay.
4. Based on the detected distance, the **buzzer behavior** is:
   - **No object detected:** Buzzer **OFF**.
   - **Object closer than 10 cm:** **Continuous beep**.
   - **Object between 10 cm and 30 cm:** **Intermittent beep** (500ms ON, 500ms OFF).
   - **Object beyond 30 cm:** Buzzer **OFF**.

---

## 2. Expected Output
| Scenario               | Distance (cm) | Buzzer Output             |
|------------------------|--------------|---------------------------|
| **No Object Detected** | 0            | OFF                       |
| **Very Close Object**  | <10          | Continuous Beep (ON)      |
| **Medium Distance**    | 10 - 30      | Beeps (500ms ON/OFF)      |
| **Far Object**         | >30          | OFF                       |
| **Object Removed**     | No reading   | OFF                       |

---

## 3. Future Enhancements
This project can be enhanced with:
- **Multiple Distance Zones:** Add more buzzer patterns for different distances.
- **Voice Alerts:** Use a **Text-to-Speech (TTS)** module for spoken alerts.
- **Bluetooth/Wi-Fi Integration:** Connect the system to a mobile app for remote monitoring.
- **Battery Optimization:** Reduce power consumption for longer operation.

---

## 4. Conclusion
This **ultrasonic obstacle detection system** provides a cost-effective, real-time solution for **visually impaired users** and other object detection applications. It is a **simple yet effective implementation** that can be further improved with additional features.



