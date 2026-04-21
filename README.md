# ESP32-Based Water Quality Monitoring System

## Overview

This project is an IoT-based water quality monitoring system built using ESP32. It continuously measures important water quality parameters and sends real-time data to the Blynk IoT dashboard for remote monitoring.

The system uses the following sensors:

* pH Sensor
* TDS Sensor (Total Dissolved Solids)
* Turbidity Sensor
* DS18B20 Temperature Sensor

It also provides a basic SAFE / UNSAFE water quality indication based on threshold values.

---

## Features

* Real-time sensor monitoring
* Blynk IoT cloud integration
* Serial Monitor live readings
* Temperature monitoring using DS18B20
* Safe / Unsafe water quality detection
* Easy calibration support
* ESP32-based low-cost implementation

---

## Hardware Used

* ESP32 Dev Board
* DFRobot Gravity TDS Sensor
* Analog pH Sensor Module
* Turbidity Sensor
* DS18B20 Waterproof Temperature Sensor
* 4.7kΩ resistor (for DS18B20)
* 7805 Power Supply Section
* Breadboard / PCB
* Jumper wires
* Regulated Power Supply

---

## Pin Connections

| Sensor           | ESP32 Pin |
| ---------------- | --------- |
| TDS Sensor       | GPIO 33   |
| pH Sensor        | GPIO 34   |
| Turbidity Sensor | GPIO 35   |
| DS18B20 Data     | GPIO 4    |

> DS18B20 requires a 4.7kΩ pull-up resistor between VCC and DATA.

---

## Software Used

* Arduino IDE
* Blynk IoT Platform
* ESP32 Board Package
* DallasTemperature Library
* OneWire Library

---

## Blynk Virtual Pins

| Parameter    | Virtual Pin |
| ------------ | ----------- |
| Temperature  | V0          |
| TDS          | V1          |
| pH           | V2          |
| Turbidity    | V3          |
| Water Status | V4          |

---

## Setup Instructions

### 1. Clone the Repository

```bash
git clone https://github.com/your-username/water-quality-monitoring-system.git
cd water-quality-monitoring-system
```

### 2. Configure Secrets

Create your local credentials file from the template:

```bash
cp secrets.example.h secrets.h
```

Then update `secrets.h` with:

* WiFi SSID
* WiFi Password
* Blynk Auth Token

Do not commit `secrets.h`.

### 3. Upload Code

* Open the project in Arduino IDE
* Select ESP32 Board
* Install required libraries
* Upload firmware to ESP32

---

## Water Quality Logic

### SAFE Condition

* pH: 6.5 to 8.5
* TDS: less than 500 ppm
* Turbidity: less than 1000

If conditions are outside these limits, the system marks water as:

## UNSAFE

---

## Future Scope

* Cloud data logging
* SMS / mobile alert notifications
* Automatic purification system trigger
* AI-based water quality prediction
* Web dashboard integration

---
caffeinboy.
