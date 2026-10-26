# STM32 MQ5 Gas Detection System

## Overview
This project implements a real-time gas monitoring system using an MQ5 gas sensor and an STM32 Nucleo development board. The system reads analog voltage from the sensor, applies digital signal processing to filter out noise, and provides both visual hardware feedback via a traffic-light LED system and live data telemetry via STM32CubeMonitor.

## Key Features
* **Analog Data Acquisition:** Continuous ADC polling to read raw voltage values from the MQ5 sensor.
* **Moving Average Filter:** A 10-element ring buffer algorithm is used to smooth the noisy raw ADC signals into a stable average value (`avg_value` / `mean_f`).
* **Traffic-Light LED Indicator:** A decoupled, threshold-based logic loop that gives real-time visual feedback based on the smoothed voltage:
  * **Green LED:** Safe levels (Mean < 1.0V)
  * **Yellow LED:** Warning levels (1.0V <= Mean < 2.0V)
  * **Red LED:** Danger/Alert levels (Mean >= 2.0V)
* **UART Debugging:** Retargeted `printf` functionality to stream serial data directly to a host PC terminal (115200 Baud, 8N1) via UART2.
* **Live Telemetry & Visualization:** Full integration with STM32CubeMonitor. By exposing variables globally in the `.elf` file, the system allows for direct memory access via ST-Link to plot both raw and averaged sensor data simultaneously in real-time.
* **Hardware Interrupt (EXTI):** Capability to capture sudden threshold spikes directly from the sensor's digital pin using a hardware interrupt.

## Hardware Setup
* **Microcontroller:** STM32 Nucleo Board 
* **Sensor:** MQ5 Gas Sensor (Analog Out connected to ADC pin, Digital Out to EXTI pin)
* **Indicators:** 3x LEDs (Green, Yellow, Red) connected to GPIO Output pins.
* **Connection:** USB to PC (provides ST-Link debugging and Virtual COM Port).

## Software & Tools
* **STM32CubeIDE:** Used for C code development, compilation, and flashing.
* **STM32CubeMonitor:** Node-RED-based dashboard used for live plotting of the C variables via the compiled `.elf` executable.
* **Git:** Version control used throughout the development process.

## How It Works
1. The `main` `while(1)` loop continuously reads the ADC value.
2. The raw value is pushed into an array (ring buffer), and the oldest value is overwritten.
3. The sum of the buffer is divided by 10 to calculate the moving average.
4. The main loop evaluates the smoothed average against predefined voltage thresholds to toggle the appropriate LED.
5. STM32CubeMonitor reads the memory addresses of the global variables `adc_value` and `avg_value` through the ST-Link and plots them dynamically, demonstrating the dampening effect of the moving average filter on sensor noise.
