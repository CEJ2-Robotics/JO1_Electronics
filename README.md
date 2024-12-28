# John Deere Tractor Navigation System - Electronics

<p align="justify">This repository contains the PCB layout for a shield-style board designed to interface with the NUCLEO-H745ZI-Q development board. The PCB integrates various components and connection interfaces required for the tractor navigation system developed in collaboration with John Deere, serving as a practical application of embedded systems concepts. The implementation details of this electronics design can be found in the <a href="https://github.com/CEJ2-Robotics/JO1_Embedded">embedded software repository</a>.</p>

## System Overview

<p align="justify">The custom PCB serves as a connection hub for the system's components, handling:
  
- Power distribution to components
- CAN interface (<b>FDCAN1</b>) for encoder data
- I2C connection (<b>I2C4</b>) for the MPU6050 IMU
- SPI interface (<b>SPI5</b>) for the nRF24L01 wireless module
- PWM signal routing (<b>TIM13</b>, <b>TIM14</b>, <b>TIM1</b>) for motors and buzzer</p>

## Power Distribution

<p align="justify">The PCB design includes three power input screw terminals. Here's our implementation from the embedded repository:</p>

### Logic Power Screw Terminals

<p align="justify">
- <b>5V terminal</b>: Connected to external LM2596 regulator outputting 5V
- <b>3.3V terminal</b>: Connected to external LM2596 regulator outputting 3.3V
- Both regulators were powered by 7.4V from two 3.7V Li-Po cells in series</p>

### STM32 Power Screw Terminal

<p align="justify">
- <b>7.4V terminal</b>: Connects directly to NUCLEO-H745ZI-Q's VIN
- Board configuration: JP2 jumper on pins 3-4
- Power specifications:
 - Input range: <b>7-11V</b>
 - Current draw varies with voltage:
   - 800mA @ 7V
   - 450mA @ 7-9V
   - 250mA @ 9-11V</p>

### ESC and STM32 Connection

<p align="justify">
- The ESC is a separate pre-built circuit with its own power connections
- Not powered through the PCB
- In our setup, we used a 7.4V Li-Po 2S battery to power both:
 - The ESC directly
 - The STM32 through the PCB's 7.4V screw terminal</p>

## Component List

| Component          | Specifications              | Purpose                   | Location               |
|------------------- |---------------------------- |-------------------------- |----------------------- |
| NUCLEO-H745ZI-Q    | Dual-core ARM Cortex-M7/M4  | Main controller           | Shield base board      |
| Arduino Nano       | ATmega328P                  | Encoder preprocessing     | On shield PCB          |
| nRF24L01           | 2.4GHz wireless module      | GPS data reception        | On shield PCB          |
| MPU6050            | 6-DOF IMU                   | Orientation tracking      | On shield PCB          |
| GM 25-370          | 12V DC motor with encoder   | Drive system              | External (pins on PCB) |
| MCP2515            | CAN controller              | CAN-SPI interface         | On shield PCB          |
| TJA1051            | CAN transceiver             | CAN physical layer        | On shield PCB          |
| MG996R             | Servo motor                 | Steering control          | External (pins on PCB) | 
| 30A ESC            | Electronic speed controller | Motor drive control       | External (pins on PCB) |
| HW-508             | Passive buzzer              | Audio feedback            | On shield PCB          |
| LM2596 (x2)        | DC-DC Step Down             | 5V and 3.3V regulation    | External (recommended) |
