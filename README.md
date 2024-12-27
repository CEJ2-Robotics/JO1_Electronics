# John Deere Tractor Navigation System - Electronics

This repository contains the electronics design and PCB layout for the autonomous tractor navigation system developed in collaboration with John Deere. The system is designed to support both internal and external navigation modes for precision agriculture applications.

## PCB Design

[PCB images to be added]

The PCB design incorporates:

- Dedicated power distribution with LM2596 voltage regulators
- CAN bus interface for encoder data transmission
- SPI interface for wireless module communication
- I2C routing for IMU sensor
- PWM signal routing for motor control

## Component List

| Component | Specifications | Purpose |
|-----------|---------------|----------|
| NUCLEO-H745ZI-Q | Dual-core ARM Cortex-M7/M4 | Main controller |
| Arduino Nano | ATmega328P | Encoder preprocessing |
| nRF24L01 | 2.4GHz wireless module | GPS data reception |
| MPU6050 | 6-DOF IMU | Orientation tracking |
| GM 25-370 | 12V DC motor with encoder | Drive system |
| MCP2515 | CAN controller | CAN-SPI interface |
| TJA1051 | CAN transceiver | CAN physical layer |
| MG996R | Servo motor | Steering control |
| 30A ESC | Electronic speed controller | Motor drive control |
| HW-508 | Passive buzzer | Audio feedback |

## Power Distribution

The system uses multiple power sources:

- 2x 3.7V Li-Po batteries (2000mAh) - Logic power
- 1x 7.4V Li-Po battery (1500mAh) - Motor power

Voltage regulation is handled by:

- 2x LM2596 step-down regulators (25W, 3A)
- Built-in voltage regulators on development boards

## Interface Specifications

### Communication Interfaces

- USART3: Debug output (115200 baud)
- I2C4: IMU communication
- SPI5: Wireless module interface
- FDCAN1: Encoder data reception

### Control Signals

- TIM13: Servo steering control (PWM)
- TIM14: ESC motor control (PWM)
- TIM1: Buzzer feedback (PWM)
