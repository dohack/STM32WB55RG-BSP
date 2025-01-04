
---

# myBlueLink STM32WB55RG Board Support Package (BSP)

## Overview

Welcome to myBlueLink, the open-source development board for BLE, Zigbee, Matter, and more! Whether you're a hobbyist, engineer, or student, myBlueLink provides a versatile platform for prototyping, experimentation, and innovation in wireless communication,based on STM32WB55RG.

The **STM32WB55RG Board Support Package (BSP)** provides a comprehensive set of hardware abstraction layers, drivers, and middleware for the **STM32WB55RG** microcontroller. This package enables rapid development of embedded applications leveraging the Bluetooth, Wi-Fi, and other peripheral capabilities of the STM32WB55 series.

### Features

- **Microcontroller Support**: STM32WB55RG
- **Middleware**: Bluetooth stack, SPI, UART, GPIO, and more
- **FreeRTOS Support**: Optionally integrated for real-time applications
- **Peripheral Drivers**: Full support for STM32 HAL drivers
- **GPIO, LED, Button APIs**: Easy interface to onboard peripherals

This BSP is ideal for developers building embedded applications using STM32CubeMX, STM32CubeIDE, or other toolchains.

---

## Table of Contents

1. [Getting Started](#getting-started)
2. [Folder Structure](#folder-structure)
3. [Dependencies](#dependencies)
4. [Build and Flash](#build-and-flash)
5. [API Usage](#api-usage)
6. [License](#license)

---

## Getting Started

### Prerequisites

Before you begin, ensure that you have the following software installed:

- **STM32CubeMX**: For configuring peripherals and generating initialization code.
- **STM32CubeIDE** or **Keil** or **IAR Embedded Workbench**: To develop and debug your application.
- **ST-Link/V2**: For flashing the firmware to the STM32WB55RG board.
- **CMake** (optional, if using a custom build system).

You will also need an STM32WB55RG development board, such as the **STM32WB55 Nucleo** or a custom board based on the STM32WB55RG.

### Cloning the BSP Repository

To get started with the BSP, clone this repository to your local machine:

```bash
git clone https://github.com/dohack/STM32WB55RG-BSP.git
cd STM32WB55RG-BSP
```

---

## Folder Structure

This repository is organized into several directories, each serving a specific purpose for hardware abstraction, peripheral control, middleware, and more.

```plaintext
STM32WB55RG_BSP/
├── Inc/                     # Header files
│   ├── stm32wb55xx.h         # MCU specific header
│   ├── stm32wbxx_hal.h       # STM32 HAL header
│   ├── board_config.h        # Board configuration header
│   ├── system_stm32wb55xx.h  # System initialization header
│   └── ...
├── Src/                     # Source files
│   ├── stm32wb55xx_hal_msp.c # HAL MSP initialization
│   ├── system_stm32wb55xx.c # System initialization
│   ├── board_config.c        # Board-specific initialization
│   ├── peripheral_init.c     # Peripheral initialization
│   └── ...
├── Middlewares/              # Middleware like Bluetooth stack
│   ├── Bluetooth/            # Bluetooth-related files
│   │   ├── ble_app.c
│   │   ├── ble_stack.c
│   │   └── ...
│   └── ...
├── Drivers/                  # STM32 HAL drivers
│   ├── STM32WBxx_HAL_Driver/ # HAL driver files for STM32WB55
│   │   ├── src/
│   │   │   ├── stm32wbxx_hal_gpio.c
│   │   │   ├── stm32wbxx_hal_uart.c
│   │   │   └── ...
│   └── ...
├── CMSIS/                    # ARM Cortex-M CMSIS files
│   ├── Core/                 # Cortex-M core files
│   │   ├── stm32wb55xx.h
│   │   └── ...
├── Utilities/                # Utility files (e.g., FreeRTOS config)
│   ├── FreeRTOS/             # FreeRTOS configuration files
│   │   ├── FreeRTOSConfig.h
│   │   └── ...
├── STM32WB55RG_BSP.h         # BSP API header file
├── STM32WB55RG_BSP.c         # BSP source file
├── README.md                 # This file
└── CMakeLists.txt            # CMake build system (optional)
```

---

## Dependencies

The STM32WB55RG BSP relies on the following:

1. **STM32 HAL Libraries**: For low-level hardware abstraction.
2. **CMSIS (Cortex-M Software Interface Standard)**: Required for core system functions.
3. **Bluetooth Stack (Optional)**: The middleware directory includes an optional Bluetooth stack if you're using Bluetooth LE functionality.
4. **FreeRTOS (Optional)**: If using an RTOS, FreeRTOS support is included with configuration files in the `Utilities/FreeRTOS` directory.

---

## Build and Flash

To build and flash your project onto the STM32WB55RG, follow these steps:

### 1. Using STM32CubeIDE

1. Open **STM32CubeIDE** and import the generated project from **STM32CubeMX**.
2. Select the target device (STM32WB55RG) and configure the necessary peripherals.
3. Click on **Build** to compile the code.
4. Connect the **ST-Link programmer** to the STM32WB55RG board.
5. Click on **Debug** or **Run** to flash the firmware to the board and start debugging.

### 2. Using Makefile / CMake (Optional)

If you're using CMake or a custom build system:

1. Navigate to the project directory and create the build environment.

   ```bash
   mkdir build
   cd build
   cmake ..
   ```

2. Build the project:

   ```bash
   make
   ```

3. Flash the firmware using ST-Link:

   ```bash
   st-flash write build/STM32WB55RG_BSP.bin 0x8000000
   ```

---

## API Usage

### 1. LED Control

The BSP provides easy-to-use functions to control onboard LEDs.

#### Initialization

```c
BSP_LED_Init();
```

#### Turning LED On/Off

```c
BSP_LED_On();   // Turns the LED on
BSP_LED_Off();  // Turns the LED off
```

### 2. Button Control

Control buttons with simple functions to initialize and check the state.

#### Initialization

```c
BSP_Button_Init();
```

#### Get Button State

```c
uint8_t buttonState = BSP_Button_GetState();
```

### 3. Bluetooth Stack (Optional)

If your project requires Bluetooth functionality, the Bluetooth stack is provided in the `Middlewares/Bluetooth/` directory.

#### Example: Bluetooth Initialization

```c
BLE_Init();
```

This will initialize the Bluetooth stack and allow you to start advertising or handling BLE events.

---

## License

This BSP is open source and provided under the **MIT License**. Feel free to modify and contribute. Please see the [LICENSE](LICENSE) file for more details.

---

## Acknowledgements

- **STMicroelectronics** for their STM32WB series microcontrollers.
- **FreeRTOS** for providing a real-time operating system.
- **ARM Cortex-M** for their efficient and powerful cores.
- **GitHub** for version control and collaborative development.

---

## Contact

For any issues or contributions, feel free to open an issue or pull request on this repository.

---

This `README.md` provides a comprehensive guide for your users, including an overview of the BSP, how to set up and build the project, and how to use the APIs. It's both informative and professional, with a clean structure for easy navigation.
