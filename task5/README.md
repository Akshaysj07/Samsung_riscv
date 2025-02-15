```markdown
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
- **Trigger Pin → GPIO Pin (Sends ultrasonic pulse)**  
- **Echo Pin → GPIO Pin (Receives reflected signal)**  

The **traffic light system** is controlled by the **RISC-V Processor** through GPIO pins:  
- **Red Light → GPIO Pin**  
- **Yellow Light → GPIO Pin**  
- **Green Light → GPIO Pin**  

## 📌 **Pin Connections**  
### **1️⃣ Ultrasonic Sensor**  
| **Sensor Pin** | **RISC-V Pin** | **Description** |  
|---------------|----------------|----------------|  
| **VCC**       | **5V**          | Power Supply  |  
| **GND**       | **GND**         | Ground        |  
| **TRIG**      | **GPIO X**      | Trigger Signal (Output) |  
| **ECHO**      | **GPIO Y**      | Echo Response (Input) |  

### **2️⃣ Traffic Light System**  
| **Traffic Light** | **RISC-V Pin** | **Description** |  
|------------------|----------------|----------------|  
| **Red Light**     | **GPIO A**      | Stop Signal |  
| **Yellow Light**  | **GPIO B**      | Prepare to Stop |  
| **Green Light**   | **GPIO C**      | Go Signal |  

## 📌 **Working Principle**  
1️⃣ **Ultrasonic sensors detect vehicle presence and send data to RISC-V processor.**  
2️⃣ **Processor analyzes data and adjusts traffic light timings dynamically.**  
3️⃣ **Traffic lights operate efficiently to manage congestion and improve traffic flow.**  

## Circuit Diagram  
![Alt Text](Traffic_Light_Controller_RISCV.PNG)
```
