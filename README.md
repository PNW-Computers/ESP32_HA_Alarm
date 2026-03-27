# 🚨 Home Assistant ESP32-Based Distributed Car Alarm System

A two-part security system: A battery-powered vibration sensor inside the vehicle and a high-decibel, mains-powered siren mounted to the house.

---

## 🏗️ System Architecture

1.  **The Trigger (Car Unit):** ESP32-S3 + SW-420 Sensor. Powered by LiPo. Sends "Vibration Detected" to HA via Wi-Fi.
2.  **The Brain (Home Assistant):** Processes the signal and checks if the system is "Armed."
3.  **The Alarm (House Unit):** ESP32-S3 + 5V Relay + 12V Siren. Plugged into a wall outlet. Triggered by HA.

---

## 🧱 Materials List

### 🚗 Unit 1: Car Sensor (Mobile)
* **LILYGO T-Display-S3**: Microcontroller.
* **SW-420 Vibration Sensor**: Detects movement/impact.
* **3.7V 2000mAh/3000mAh LiPo**: Portable power.
* **5V Charge/Discharge Module**: Manages battery and boosts to 5V.

### 🏠 Unit 2: House Siren (Mains Powered)
* **LILYGO T-Display-S3**: Microcontroller & Status Display.
* **5V 1-Channel Relay Module**: (HiLetgo or similar with Optocoupler).
* **12V DC Power Supply**: 2A "Wall Wart" adapter.
* **12V DC Outdoor Siren**: 110dB+ high-decibel alarm.
* **USB Power Block**: To power the ESP32.

---

## 🔌 Wiring Diagrams

### House Siren Unit Wiring


1.  **ESP32 to Relay:**
    * **5V/VBUS Pin** ➔ Relay **VCC**
    * **GND Pin** ➔ Relay **GND**
    * **GPIO 12** ➔ Relay **IN**
2.  **Relay to Siren Circuit:**
    * 12V Adapter **(+)** ➔ Relay **COM** (Center Terminal)
    * Relay **NO** (Normally Open) ➔ Siren **(+)**
    * 12V Adapter **(-)** ➔ Siren **(-)** (Direct Connection)

---

## 💻 ESPHome Configuration (House Unit)

```yaml
# Partial Config for the House Siren Display & Relay
esphome:
  name: house_siren

display:
  - platform: st7789v
    # ... (Display timings for T-Display S3)
    lambda: |-
      if (id(siren_relay).state) {
        it.fill(Color::RED);
        it.print(160, 85, id(font_large), "!!! ALARM !!!");
      } else {
        it.fill(Color::BLACK);
        it.print(160, 85, id(font_small), "SYSTEM READY");
      }

switch:
  - platform: gpio
    pin: 12
    name: "House Siren Relay"
    id: siren_relay
```

---

## 🤖 Home Assistant Automation Logic

```yaml
alias: "Global Alarm: Car Vibration -> House Siren"
trigger:
  - platform: state
    entity_id: binary_sensor.car_vibration_sensor
    to: "on"
condition:
  - condition: state
    entity_id: input_boolean.alarm_system_armed
    state: "on"
action:
  - service: switch.turn_on
    target:
      entity_id: switch.house_siren_relay
  - delay: "00:02:00"
  - service: switch.turn_off
    target:
      entity_id: switch.house_siren_relay
```

---

## ⚠️ Technical Notes
* **Safety:** Only switch the **12V DC** side with the relay. Do not attempt to switch 120V/240V AC unless you are an experienced electrician.
* **Reliability:** The House Unit should have a static IP or a strong Wi-Fi connection to ensure it receives the "Turn On" command instantly from Home Assistant.
