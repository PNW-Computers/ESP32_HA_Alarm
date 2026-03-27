# 🚨 ESP32 Car Security
## Home Assistant Distributed Car & Motion Alarm System (Sensor, Siren & Kill Switch)

![PNWC Car Alarm Project Header](./esp32alarm.png)

A high-performance, distributed vehicle security system that bridges a battery-powered mobile sensor unit with a mains-powered house siren via Home Assistant and ESPHome.

---

## 🏗️ System Architecture

1.  **The Sensor (Car Unit):** A LILYGO T-Display S3 equipped with an **LD2410C Human Presence Radar** and an **SW-420 Vibration Sensor**. It uses deep sleep to conserve battery and wakes instantly on vibration to report to Home Assistant.
2.  **The Brain (Home Assistant):** Processes logic, manages arm/disarm states, integrates with **Frigate NVR** for camera snapshots, and handles mobile notifications.
3.  **The Alarm (House Unit):** A second LILYGO T-Display S3 that controls a **12V DC Siren** via a 5V Relay. It features a hardwired "Wall Kill" button for emergency silencing and disarming.

---

## 📂 Repository Structure

* `car_security_tdisplay_s3.yaml`: ESPHome config for the mobile sensor unit (Vibration + Radar + Battery Mgmt).
* `house_siren_tdisplay_s3.yaml`: ESPHome config for the siren controller and status display.
* `ha_automations.yaml`: The logic connecting the two units, including Frigate alerts and auto-arming.
* `zigbee_kill_button.yaml`: Optional automation for remote Zigbee-based silencing.

---

## 🔌 Hardware & Wiring

### 🏠 House Siren Unit (Unit 2)
| Component | Pin / Connection |
| :--- | :--- |
| **Relay IN** | GPIO12 |
| **Wall Kill Button** | GPIO13 ➔ GND |
| **Siren Power** | 12V DC (Switched via Relay COM/NO) |
| **Status Display** | Built-in ST7789 (SPI) |

### 🚗 Car Sensor Unit (Unit 1)
| Component | Pin / Connection |
| :--- | :--- |
| **SW-420 (Wake)** | GPIO1 |
| **LD2410C TX/RX** | GPIO3 / GPIO2 |
| **Battery ADC** | GPIO4 (via 100k/100k Divider) |

---

## 🤖 Key Features

* **Human Presence Radar:** Uses mmWave to distinguish between a cat jumping on the car (vibration only) and a person standing inside/near the vehicle (presence).
* **Intelligent Power:** Car unit enters deep sleep if no presence is detected, waking only on physical disturbance.
* **Visual Feedback:** The T-Display screens provide real-time status (RSSI, Uptime, Battery, and Alarm State).
* **Hardwired Fail-safe:** A physical button wired to the house unit can kill the siren and disarm the system even if Home Assistant or Wi-Fi is lagging.

---

## ⚠️ Safety Note
The house siren unit switches **12V DC only**. Do not attempt to switch mains AC (120V/240V) directly with the hobbyist relay modules provided in this project.
