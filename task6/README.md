# Ultrasonic Obstacle Detection using VSDSquadron Mini

## Overview
This project implements an **ultrasonic obstacle detection system** using an **HC-SR04 ultrasonic sensor** and an **active buzzer** on the **VSDSquadron Mini Board**. The system detects obstacles and provides **audible alerts** based on distance.

---
## Code implementation

#include <ch32v00x.h>

// Define GPIO pins
#define RED_LED     GPIO_Pin_3  // PC3 (A < B)
#define GREEN_LED   GPIO_Pin_4  // PC4 (A == B)
#define YELLOW_LED  GPIO_Pin_5  // PC5 (A > B)
#define BUZZER      GPIO_Pin_6  // Example: PC6
#define LASER_SENSOR GPIO_Pin_0  // PD0 (Example sensor input)

void GPIO_Config(void) {
    GPIO_InitTypeDef GPIO_InitStructure;

    // Enable GPIO clocks for port C and D
    RCC_APB2PeriphClockCmd(RCC_APB2Periph_GPIOC, ENABLE);
    RCC_APB2PeriphClockCmd(RCC_APB2Periph_GPIOD, ENABLE);

    // Configure LED and buzzer as output
    GPIO_InitStructure.GPIO_Pin = RED_LED | GREEN_LED | YELLOW_LED | BUZZER;
    GPIO_InitStructure.GPIO_Mode = GPIO_Mode_Out_PP;
    GPIO_InitStructure.GPIO_Speed = GPIO_Speed_50MHz;
    GPIO_Init(GPIOC, &GPIO_InitStructure);

    // Configure laser sensor as input
    GPIO_InitStructure.GPIO_Pin = LASER_SENSOR;
    GPIO_InitStructure.GPIO_Mode = GPIO_Mode_IPU;  // Pull-up input
    GPIO_Init(GPIOD, &GPIO_InitStructure);
}

void DelayMs(uint32_t ms) {
    Delay_Ms(ms);  // Use built-in delay function
}

void TrafficSignalControl(void) {
    while (1) {
        uint8_t laser = GPIO_ReadInputDataBit(GPIOD, LASER_SENSOR);

        // Step 1: Red light on
        GPIO_SetBits(GPIOC, RED_LED);
        GPIO_ResetBits(GPIOC, GREEN_LED | YELLOW_LED);
        if (laser == 0) GPIO_SetBits(GPIOC, BUZZER);
        else GPIO_ResetBits(GPIOC, BUZZER);
        DelayMs(5000);

        // Step 2: Red & Yellow light on
        GPIO_SetBits(GPIOC, RED_LED | YELLOW_LED);
        GPIO_ResetBits(GPIOC, GREEN_LED);
        if (laser == 0) GPIO_SetBits(GPIOC, BUZZER);
        else GPIO_ResetBits(GPIOC, BUZZER);
        DelayMs(2000);

        // Step 3: Green light on
        GPIO_SetBits(GPIOC, GREEN_LED);
        GPIO_ResetBits(GPIOC, RED_LED | YELLOW_LED | BUZZER);
        DelayMs(5000);

        // Step 4: Yellow light on
        GPIO_SetBits(GPIOC, YELLOW_LED);
        GPIO_ResetBits(GPIOC, RED_LED | GREEN_LED);
        if (laser == 0) GPIO_SetBits(GPIOC, BUZZER);
        else GPIO_ResetBits(GPIOC, BUZZER);
        DelayMs(2000);
    }
}

int main(void) {
    SystemCoreClockUpdate();
    Delay_Init();
    GPIO_Config();

    TrafficSignalControl();

    return 0;
}


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



