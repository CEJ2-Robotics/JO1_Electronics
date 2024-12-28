# John Deere Tractor Navigation System - Electronics

<p align="justify"> This repository contains the PCB layout for a <strong>shield-style board</strong> designed to interface with the NUCLEO-H745ZI-Q development board. The PCB integrates various components and connection interfaces required for the tractor navigation system developed in collaboration with John Deere, serving as a practical application of embedded systems concepts. The implementation details of this electronics design can be found in the embedded software repository.</p>

## System Overview

<p align="justify">The custom PCB serves as a connection hub for the system's components, handling:</p>

<ul>
  <li><strong>Power distribution to components</strong></li>
  <li><strong>CAN interface (FDCAN1)</strong> for encoder data</li>
  <li><strong>I2C connection (I2C4)</strong> for the MPU6050 IMU</li>
  <li><strong>SPI interface (SPI5)</strong> for the nRF24L01 wireless module</li>
  <li><strong>PWM signal routing (TIM13, TIM14, TIM1)</strong> for motors and buzzer</li>
</ul>

## Power Distribution

<p align="justify">The PCB design includes three power input screw terminals. Here's our implementation from the embedded repository:</p>

### Logic Power Screw Terminals

<ul>
  <li><strong>5V terminal:</strong> Connected to external LM2596 regulator outputting 5V</li>
  <li><strong>3.3V terminal:</strong> Connected to external LM2596 regulator outputting 3.3V</li>
  <li>Both regulators were powered by 7.4V from two 3.7V Li-Po cells in series</li>
</ul>

### STM32 Power Screw Terminal

<ul>
  <li><strong>7.4V terminal:</strong> Connects directly to NUCLEO-H745ZI-Q's VIN</li>
  <li><strong>Board configuration:</strong> JP2 jumper on pins 3-4</li>
  <li><strong>Power specifications:</strong>
    <ul>
      <li><strong>Input range:</strong> 7-11V</li>
      <li><strong>Current draw varies with voltage:</strong></li>
      <ul>
        <li>800mA @ 7V</li>
        <li>450mA @ 7-9V</li>
        <li>250mA @ 9-11V</li>
      </ul>
    </ul>
  </li>
</ul>

### ESC and STM32 Connection

<ul>
  <li>The <strong>ESC</strong> is a separate pre-built circuit with its own power connections and is not powered through the PCB.</li>
  <li>In our setup, we used a <strong>7.4V Li-Po 2S battery</strong> to power both:
    <ul>
      <li>The <strong>ESC</strong> directly</li>
      <li>The <strong>STM32</strong> through the PCB's 7.4V screw terminal</li>
    </ul>
  </li>
</ul>

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
