# 🚨 PNWC Car Security — Home Assistant Distributed Alarm

<p align="center">
  <img src="esp32alarm.png" width="800" alt="PNWC Car Alarm Project Collage">
</p>

A professional-grade, distributed vehicle security system. This project bridges a battery-powered mobile sensor unit with a mains-powered house siren using Home Assistant and ESPHome.

---

## 🏗️ System Architecture

1.  **The Sensor (Car Unit):** A LILYGO T-Display S3 equipped with an **LD2410C Human Presence Radar** and an **SW-420 Vibration Sensor**. Wakes instantly on disturbance.
2.  **The Brain (Home Assistant):** Manages logic, arm/disarm states, and **Frigate NVR** integration.
3.  **The Alarm (House Unit):** A second T-Display S3 controlling a **12V DC Siren** via a 5V Relay, featuring a hardwired "Wall Kill" button.

---

## 📂 Repository Structure

* `car_security_tdisplay_s3.yaml`: Sensor unit config (Vibration + Radar + Battery).
* `house_siren_tdisplay_s3.yaml`: Siren controller with status display and wall-button logic.
* `ha_automations.yaml`: Global logic, notifications, and camera triggers.
* `zigbee_kill_button.yaml`: Optional Zigbee remote integration.

---

## 🛠️ 3D Enclosure & Mounting Designs

The system requires specific mounting to ensure sensor accuracy and weather resistance. Use the blueprint below for printing and assembly.

<p align="center">
  <img src="alarm_3d_case_designs.svg" width="800" alt="3D Enclosure Blueprints">
</p>

### Enclosure Specifications

| Feature | Car Sensor Unit | House Siren Unit |
| :--- | :--- | :--- |
| **Material** | PETG (Heat tolerant for interiors) | ASA (UV & Weather stable) |
| **Infill** | 25% Gyroid | 40% Gyroid |
| **Mounting** | Under-seat rail / Hook tabs | M6 Concrete Anchors |
| **Hardware** | M3 Heat-set inserts x 4 | M3 Heat-set / M6 Bolts |

**Key Design Note:** The outdoor siren bracket includes a **15° down-tilt** to maximize audio projection toward the driveway and prevent water ingress into the horn.

---

## 🔌 Hardware & Wiring

### 🏠 House Siren Unit (Unit 2)
* **Relay IN:** GPIO12
* **Wall Kill Button:** GPIO13 ➔ GND (Internal Pullup)
* **Status Display:** Built-in ST7789 (`invert: true` may be required for correct colors)

### 🚗 Car Sensor Unit (Unit 1)
* **SW-420 (Wake):** GPIO1
* **LD2410C TX/RX:** GPIO3 / GPIO2
* **Battery ADC:** GPIO4 (via 100k/100k Divider)

---

## 🤖 Advanced Features

* **mmWave Detection:** Radar distinguishes between environmental vibration and actual human presence inside the cabin.
* **Intelligent Deep Sleep:** Car unit draws minimal current until the SW-420 triggers a wake event.
* **Manual Overrides:** Three kill levels: Local (display), Wall (hardwired), and Mobile (HA App).

---

## ⚠️ Safety Note
The house unit is designed to switch **12V DC only**. Switching mains AC (120V/240V) with these components is dangerous and not supported by this documentation.
