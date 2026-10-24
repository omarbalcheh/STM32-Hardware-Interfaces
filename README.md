# STM32 Hardware Interfaces

This repository contains a growing collection of embedded bare-metal and HAL-based projects demonstrating hardware bring-up, custom driver development, and sensor integration on STM32 microcontrollers. 

Instead of a monolithic codebase, this repository is structured as a monorepo. Each folder represents a self-contained project focusing on different hardware peripherals (ADC, I2C, SPI, UART) and includes custom C-drivers, hardware verification, and logic analyzer diagnostics.

**Project Modules**

*   **[STM32-Gas-Detection-MQ5](./STM32-Gas-Detection-MQ5):** Implementation of ADC readout, calibration logic, and signal processing for the MQ5 gas sensor.
*   *(Additional sensor and interface projects will be added as they are completed)*

**Hardware & Tech Stack**

*   **Microcontrollers:** STM32L432KC (Nucleo-32)
*   **Languages:** C
*   **Frameworks & Tools:** STM32 HAL, STM32CubeIDE
*   **Testing:** Logic Analyzer (PulseView/Saleae) for protocol verification

**Repository Structure**

Each sub-folder contains a complete, standalone STM32CubeIDE project. Detailed hardware setups, wiring diagrams, and logic analyzer signal screenshots can be found in the specific `README.md` inside each project folder.
