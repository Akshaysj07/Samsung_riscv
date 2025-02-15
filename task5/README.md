# Traffic Light Controller Using Ultrasonic Sensors in RISC-V Processor

## **Overview**  
A RISC-V-based traffic light controller utilizes **ultrasonic sensors** to detect vehicle presence and density, dynamically adjusting signal timing to optimize traffic flow, reduce congestion, enhance safety, and improve overall intersection efficiency.  

## **Components Required**  
- **RISC-V Processor**  
- **Ultrasonic Sensors**  
- **Traffic Light System (LEDs or Relays)**  
- **Power Supply**  
- **Resistors and Jumper Wires**  

## **Circuit Connection**  
The **ultrasonic sensors** are connected to the **RISC-V Processor** as follows:  
- **VCC (Power) → 5V pin** on the processor board  
- **GND (Ground) → GND pin** on the board  
- **Trigger Pin → GPIO 10 (Sends ultrasonic pulse)**  
- **Echo Pin → GPIO 11 (Receives reflected signal)**  

The **traffic light system** is controlled by the **RISC-V Processor** through GPIO pins:  
- **Red Light → GPIO 2**  
- **Yellow Light → GPIO 3**  
- **Green Light → GPIO 4**  

## 📌 **Pin Connections**  
### **1️⃣ Ultrasonic Sensor**  
| **Sensor Pin** | **RISC-V Pin** | **Description** |  
|---------------|----------------|----------------|  
| **VCC**       | **5V**          | Power Supply  |  
| **GND**       | **GND**         | Ground        |  
| **TRIG**      | **GPIO 10**     | Trigger Signal (Output) |  
| **ECHO**      | **GPIO 11**     | Echo Response (Input) |  

### **2️⃣ Traffic Light System**  
| **Traffic Light** | **RISC-V Pin** | **Description** |  
|------------------|----------------|----------------|  
| **Red Light**     | **GPIO 2**      | Stop Signal |  
| **Yellow Light**  | **GPIO 3**      | Prepare to Stop |  
| **Green Light**   | **GPIO 4**      | Go Signal |  

## 📌 **Working Process**  
### *Step-by-Step Working of the Traffic Light System with Buzzer & Laser Sensor*  
This system simulates a *traffic light sequence* and uses a *laser sensor* to detect obstructions. If an obstruction is detected, a *buzzer* will alert the user.  

### *1️⃣ System Initialization*  
- The *RISC-V Processor* initializes and configures the *GPIO pins*.  
- *LEDs (Red, Yellow, Green) & Buzzer* are set as *output*.  
- *Laser Sensor* is set as *input* (GPIO 12).  

### *2️⃣ Main Working Loop*  
The system runs in a continuous loop, executing the *traffic light sequence*:  

#### *🔴 Step 1: Red Light ON (Stop)*  
- *Red LED (GPIO 2) turns ON*.  
- *Yellow & Green LEDs remain OFF*.  
- *Laser Sensor checks for obstruction*:  
  - If *no obstruction (Laser Sensor = 1)* → Buzzer OFF.  
  - If *obstruction detected (Laser Sensor = 0)* → Buzzer ON.  
- *Delay:* 5 seconds.  

#### *🟠 Step 2: Red + Yellow Light ON (Prepare to Go)*  
- *Red LED (GPIO 2) & Yellow LED (GPIO 3) turn ON*.  
- *Green LED remains OFF*.  
- *Laser Sensor checks for obstruction*:  
  - If *no obstruction* → Buzzer OFF.  
  - If *obstruction detected* → Buzzer ON.  
- *Delay:* 2 seconds.  

#### *🟢 Step 3: Green Light ON (Go)*  
- *Green LED (GPIO 4) turns ON*.  
- *Red & Yellow LEDs turn OFF*.  
- *Buzzer turns OFF regardless of the laser sensor*.  
- *Delay:* 5 seconds.  

#### *🟠 Step 4: Yellow Light ON (Slow Down)*  
- *Only Yellow LED (GPIO 3) turns ON*.  
- *Red & Green LEDs remain OFF*.  
- *Laser Sensor checks for obstruction*:  
  - If *no obstruction* → Buzzer OFF.  
  - If *obstruction detected* → Buzzer ON.  
- *Delay:* 2 seconds.  

### *3️⃣ Repeat Cycle*  
- The sequence *repeats indefinitely* every *14 seconds*.  
- *If an obstruction is detected* at any step *except when Green is ON, the **buzzer will sound an alert***.  

### *Final Behavior Summary*  
- *Normal Traffic Flow:* Follows *Red → Red+Yellow → Green → Yellow → Red*.  
- *Buzzer Alerts:* Sounds *only during Red, Red+Yellow, and Yellow* if an obstruction is detected.  
- *Green Light Priority:* The *buzzer is always OFF when the Green LED is ON.*  

## Circuit Diagram  
![Alt Text](Traffic_Light_Controller_RISCV.PNG)
```

