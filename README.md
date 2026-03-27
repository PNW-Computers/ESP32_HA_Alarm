# 🚨 ESP32 Security System — Home Assistant Distributed Alarm System

<p align="center">
  <img src="esp32alarm.png" width="800" alt="PNWC Car Alarm Project Collage">
</p>

A professional-grade, distributed vehicle security system. This project bridges a battery-powered mobile sensor unit with a mains-powered house siren using Home Assistant and ESPHome.

---

## 🏗️ System Architecture

1.  **The Sensor (Car Unit):** A **LILYGO T-Display S3** with **LD2410C Human Presence Radar** and an **SW-420 Vibration Sensor**. Automatically charges via a switched USB source; enters deep sleep 30 seconds after the car is parked to preserve LiPo health.
2.  **The Brain (Home Assistant):** Manages global logic, time-of-day scheduling, and **Frigate NVR** camera integration.
3.  **The Alarm (House Unit):** A headless **ESP32-WROOM-32** controlling a **12V DC Siren** via a 5V Relay. Features a high-reliability hardwired "Wall Kill" button.

---

## 📂 Repository Structure

* `car_security_tdisplay_s3.yaml`: Sensor unit config (Vibration + Radar + Power Management).
* `house_siren_wroom32.yaml`: Headless siren controller with "Safe Pin" relay logic and status LED.
* `ha_automations.yaml`: Main Home Assistant logic, scheduling, and notification engine.
* `frigate_notify_automate.yaml`: Advanced automation for sending Frigate video clips on trigger.
* `dashboard.md`: Full UI configuration (Mushroom Cards) for the security console.
* `system_control_card.yaml`: Raw YAML for the main dashboard status and control card.
* `frigate_live_view.yaml`: Dashboard configuration for real-time camera integration.
* `frigate_nvr_integrate.md`: Documentation for connecting Frigate events to the alarm triggers.
* `zigbee_kill_button.yaml`: Optional automation for remote Zigbee-based silencing.
* `alarm_3d_case_designs.svg`: Blueprints for PETG (Car) and ASA (Siren) enclosures.

---

## 🛒 Parts List & Shopping Links

### 🚗 Unit 1: Car Sensor (Presence & Vibration)
* **ESP32 Microcontroller:** [LILYGO T-Display S3](https://a.co/d/0gzxxSAu) (Dual-core ESP32-S3 with 1.9" LCD)
* **Presence Sensor:** [LD2410C mmWave Radar](https://a.co/d/06LWMXAf) 
* **Vibration Sensor:** [SW-420 Motion Sensor](https://a.co/d/02E32HKW)
* **LiPo Battery:** [3.7V 2000mAh LiPo Battery](https://a.co/d/0hEXVDKv) (JST 1.25mm)
* **Car Power Interface:** [12V to USB-C Step-Down Converter](https://a.co/d/03p8YRCy) OR [Low-Profile USB Adapter](https://a.co/d/03B6qD6h)
* **USB Cable:** [90-Degree Right Angle USB-C Cable](https://a.co/d/06fP6O8w)

### 🏠 Unit 2: House Siren (Relay Controlled)
* **ESP32 Microcontroller:** [ESP32-WROOM-32 DevKit](https://a.co/d/05z59KT6) (Standard 30-pin)
* **5V Relay:** [5V One-Channel Relay Module](https://a.co/d/0aWROudj) (Opto-isolated)
* **12V Siren:** [12V DC Wired Indoor/Outdoor Siren](https://a.co/d/06rncyCy)
* **Siren Power:** [12V 2A DC Power Supply Adapter](https://a.co/d/0imZnCsy)
* **Siren Kill Switch:** [Push Button Switch](https://a.co/d/031p9keo) (For "Wall Kill" extension)

---

## 🔌 Master Wiring Reference

### 🏠 Unit 2: House Siren (WROOM-32 DevKit)
| Component | ESP32 Pin | Logic / Notes |
| :--- | :--- | :--- |
| **Relay VCC** | **5V / VIN** | Powers the relay coil |
| **Relay GND** | **GND** | Common ground |
| **Relay IN** | **GPIO 13** | Trigger (Safe pin) |
| **Wall Kill Button** | **GPIO 14** | Connect to GND to trigger |
| **Status LED** | **GPIO 2** | Internal Blue LED (Pulses on Alarm) |

### 🚗 Unit 1: Car Sensor (LILYGO T-Display S3)
| Component | ESP32 Pin | Logic / Notes |
| :--- | :--- | :--- |
| **Vibration (SW-420)** | **GPIO 1** | **Hardware Wake-up Pin** |
| **Radar TX (LD2410)** | **GPIO 3** | ESP RX ← Sensor TX |
| **Radar RX (LD2410)** | **GPIO 2** | ESP TX → Sensor RX |
| **Battery Voltage** | **GPIO 4** | 100k/100k Voltage Divider |
| **USB Power Sense** | **GPIO 43** | **Internal** (Auto-Sleep Logic) |
| **LCD Backlight** | **GPIO 38** | **Internal** (Screen Dimming) |

---

## 🤖 Advanced Features

### 📡 Intelligent Power Management
The Car Unit is designed for **Zero-Maintenance Operation**:
* **Ignition Sync:** Detects USB power (GPIO43), stays awake, and charges.
* **Parked Security:** Enters Deep Sleep 30s after car off. Wakes on vibration to alert Home Assistant.

### 🔘 Triple-Layer Kill Switch
1.  **Local Display:** Dashboard controls in Home Assistant.
2.  **Hardwired:** GPIO14 physical "Wall Kill" button on the siren unit.
3.  **Mobile:** Actionable video notifications on your phone.

---

## 🧪 Testing & Commissioning

1.  **Radar Calibration:** Tune LD2410 Gate Sensitivity in ESPHome to ignore movement outside car glass.
2.  **Power Logic:** Unplug USB-C; verify the unit enters Deep Sleep and wakes on movement.
3.  **Siren Safety:** Verify the 60-second auto-timeout script works to prevent permanent siren noise.

---

## ⚠️ Safety Note
The house unit switches **12V DC only**. Do not attempt to switch mains AC (120V/240V) directly with these relay modules. Ensure all 12V lines are fused.
