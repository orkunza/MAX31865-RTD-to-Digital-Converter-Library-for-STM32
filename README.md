# MAX31865 RTD-to-Digital Converter Library for STM32

This library provides an easy-to-use interface for integrating the **MAX31865 RTD-to-Digital Converter** with STM32 microcontrollers using SPI communication.

## 🛠️ How to Use This Library

### 1️⃣ Project Configuration
- In STM32CubeIDE or your preferred STM32 development environment, enable the SPI peripheral.
- Set **"General peripheral initialization as a pair of '.c/.h' file per peripheral"** in project settings.

### 2️⃣ SPI Configuration
- Ensure SPI is **enabled** in your STM32 project.
- Configure the following SPI settings:
  - **Clock Speed:** Below **2 MHz** (for stable communication)
  - **Bit Order:** **MSB First**
  - **Clock Polarity (CPOL):** **LOW**
  - **Clock Phase (CPHA):** **2nd Edge (Falling Edge)**

### 3️⃣ Chip Select (CS) Pin Setup
- Configure a **GPIO pin** as an **Output** to act as the **Chip Select (CS)** for the MAX31865.

### 4️⃣ Adding the Library to Your Project
- Copy and include both the **header (.h) file** and **source (.c) file** of this library into your STM32 project.

📌 Example Code
Below is a basic example demonstrating how to initialize and read temperature from a PT100 sensor using MAX31865 with STM32.
```
#include "MAX31865.h"

/* Declare static variables for global scope */
MAX31865_t pt100 = {
    .spi       = &hspi1,
    .cs_gpio   = SPI1_CS_GPIO_Port,
    .cs_pin    = SPI1_CS_Pin,
    .num_wires = MAX31865_2_WIRE,      // Options: MAX31865_2_WIRE, MAX31865_3_WIRE, MAX31865_4_WIRE
    .filter_hz = MAX31865_SAMPLE_50HZ  // Options: MAX31865_SAMPLE_50HZ, MAX31865_SAMPLE_60HZ
};

float pt100Temp;

int main()
{
  /* Initialize the MAX31865 sensor */
  Max31865_Init(&pt100);

  while(1)
  {
      Max31865_ReadTempC(&pt100, &pt100Temp);
      HAL_Delay(1000);
  }
}
```

⚠️ Important Notes
Ensure proper connections between your STM32 and the MAX31865 module.
The SPI clock should not exceed 2 MHz to maintain reliable communication.
The CS pin must be manually managed when using SPI.

✅ This library simplifies the process of reading temperature from PT100/PT1000 RTD sensors using the MAX31865 chip and an STM32 microcontroller.

🔗 License: MIT
