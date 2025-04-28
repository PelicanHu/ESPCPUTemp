# ESPCPUTemp Arduino Library

![GitHub release (latest by date)](https://img.shields.io/github/v/release/PelicanHu/ESPCPUTemp?style=flat-square)
![GitHub license](https://img.shields.io/github/license/PelicanHu/ESPCPUTemp?style=flat-square)

The **ESPCPUTemp** library provides a simple and unified interface to read the internal CPU temperature sensor on Espressif ESP32-based microcontrollers. It supports both legacy and new temperature sensor drivers, ensuring compatibility across various ESP32 variants, including ESP32, ESP32-S2, ESP32-S3, ESP32-C3, ESP32-C6, and ESP32-H2.

## Features
- **Unified Interface**: Seamlessly supports both legacy (ESP32) and new (ESP32-S2/S3/C3/C6/H2) temperature sensor drivers.
- **Automatic Chip Detection**: Automatically detects the ESP32 chip model and selects the appropriate driver.
- **Error Handling**: Robust error handling with detailed Serial output for debugging.
- **Lightweight**: Minimal memory footprint, optimized for Arduino environments.
- **Cross-Platform**: Compatible with multiple ESP32 variants using the Arduino core.

## Supported Devices
| Chip Model       | Driver Type |
|------------------|-------------|
| ESP32 (D0WD, V3, etc.) | Legacy      |
| ESP32-S2         | New         | 
| ESP32-S3         | New         |
| ESP32-C3         | New         |
| ESP32-C6         | New         |
| ESP32-H2         | New         |

## Installation

### Using Arduino Library Manager
1. Open the Arduino IDE.
2. Go to **Sketch > Include Library > Manage Libraries**.
3. Search for `ESPCPUTemp`.
4. Click **Install** to download and install the library.

### Manual Installation
1. Download the latest release from the [GitHub Releases page](https://github.com/PelicanHu/ESPCPUTemp/releases).
2. Extract the `.zip` file.
3. Move the `ESPCPUTemp` folder to your Arduino libraries directory:
   - **Windows**: `C:\Users\<YourUsername>\Documents\Arduino\libraries`
   - **MacOS/Linux**: `~/Documents/Arduino/libraries`
4. Restart the Arduino IDE.

## Dependencies
- **Arduino core for ESP32**: Version 2.0.0 or higher (recommended: 3.2.0 or later).
  - Install via the Arduino Boards Manager by searching for `esp32` and selecting the Espressif Systems package.
- No additional external libraries are required.

## Usage

### Basic Example
The following example demonstrates how to initialize the temperature sensor and read the CPU temperature:

```cpp
#include <ESPCPUTemp.h>

ESPCPUTemp tempSensor;

void setup() {
  Serial.begin(115200);
  delay(100);

  if (tempSensor.begin()) {
    Serial.println("Temperature sensor initialized successfully");
  } else {
    Serial.println("Failed to initialize temperature sensor");
  }
}

void loop() {
  if (tempSensor.tempAvailable()) {
    float temp = tempSensor.getTemp();
    if (!isnan(temp)) {
      Serial.print("CPU Temperature: ");
      Serial.print(temp);
      Serial.println(" °C");
    } else {
      Serial.println("Failed to read temperature");
    }
  }
  delay(5000); // Read every 5 seconds
}
