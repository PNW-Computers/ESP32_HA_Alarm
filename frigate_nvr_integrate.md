# 📹 Frigate Intruder Event — Video Notification Automation

This automation triggers when **Unit 1 (Car Sensor)** confirms presence while the system is armed. It captures a 10-second video clip from your **Frigate NVR** and sends it as a high-priority actionable notification to your mobile device.

### 🤖 Automation YAML (Add to `automations.yaml`)

```yaml
alias: "Car Alarm - Frigate Video Notification"
description: "Sends a 10-second video clip when presence is confirmed in the vehicle."
id: car_alarm_frigate_video
mode: single

trigger:
  - platform: state
    entity_id: binary_sensor.car_security_sensor_car_presence
    to: "on"

condition:
  - condition: state
    entity_id: input_boolean.car_alarm_armed
    state: "on"
  - condition: state
    entity_id: binary_sensor.car_security_sensor_car_vibration
    state: "on"

action:
  # 1. Start a 10-second recording buffer
  - service: switch.turn_on
    target:
      entity_id: switch.frigate_driveway_record
  
  # 2. Wait for the event to be processed by Frigate
  - delay: "00:00:05"

  # 3. Send the notification with the live clip
  - service: notify.mobile_app_your_phone
    data:
      title: "🚨 INTRUDER DETECTED"
      message: "Human presence confirmed in car. Reviewing footage..."
      data:
        # This uses the Frigate API to pull the most recent event clip
        url: "/api/frigate/notifications/{{ trigger.entity_id }}/clip.mp4"
        clickAction: "/lovelace-security/car-details" # Adjust to your dashboard path
        attachment:
          url: "/api/frigate/notifications/{{ trigger.entity_id }}/thumbnail.jpg"
          content-type: jpeg
          hide-thumbnail: false
        push:
          category: "camera" # Enables the live view expansion on iOS/Android
        entity_id: camera.driveway
        actions:
          - action: DISARM_CAR_ALARM
            title: "False Alarm (Disarm)"
          - action: TRIGGER_SIREN
            title: "Panic (Sound Siren)"

  # 4. Optional: Keep recording for 2 minutes after the trigger
  - delay: "00:02:00"
  - service: switch.turn_off
    target:
      entity_id: switch.frigate_driveway_record
```

---

### 💡 Implementation Notes

1.  **Notification Action Links:** The `url` field in the notification data uses the Frigate integration proxy. Ensure your Home Assistant instance is accessible via a public URL (Nabu Casa or Cloudflare) if you want to view the clip while away from home.
2.  **Notification Category:** Setting the `category: "camera"` allows you to long-press the notification on your phone to see a live stream or the clip directly without opening the full app.
3.  **Cooldown:** The `mode: single` ensures that if the person is moving around in the car, you don't get 50 notifications in a row. It will finish the 2-minute recording before it's ready to trigger again.

---

### ✅ Project Complete
You now have a fully integrated, multi-device security stack:
* **Edge Hardware:** Low-power S3 for sensing and WROOM-32 for high-current switching.
* **Network Intelligence:** ESPHome for local logic and Home Assistant for global orchestration.
* **Visual Evidence:** Frigate NVR for event-based recording and mobile delivery.
* **User Interface:** Mushroom-based dashboard with a "Panic Mode" conditional layout.

**Is there anything else you'd like to refine before you finalize the repository?** I can help you create a **"Security Best Practices"** section for the README that discusses how to obscure the SSID of the alarm network for even more stealth.
