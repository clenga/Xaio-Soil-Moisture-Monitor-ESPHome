# ESPHome Configs

- Personal ESPHome device configuration for Xaio Soil Moisture Monitor. I found the stock firmware to be too basic and generic.
- I think something in the yaml prior to version 3.5 was causing issues during the flashing procedure so I suggest not using those.
- This yaml file is a mix of the stock code from seed studio, revisions from myself, and also some fixes and/or suggestions from claude. If that bothers you then feel free not to use the code.

## Devices

### XIAO Soil Moisture Monitor
**File:** `soil-moisture-monitor-v3.5.yaml`  
**Hardware:** Seeed Studio XIAO Soil Moisture Sensor (XIAO ESP32-C6)  
**Firmware:** v3.x (ESPHome 2026.5.1)

Enhanced firmware for the Seeed Studio XIAO Soil Moisture Sensor. Replaces the stock 3-state moisture indicator of "Normal, Almost Dry, and Dry"; with a calibrated 0–100% moisture percentage.

**Improvements over stock firmware:**
- Real moisture percentage (0–100%) via calibrated ADC
- Raw voltage sensor exposed for per-unit calibration
- Battery voltage + battery percentage entity
- Adaptive deep sleep matching stock intervals (8h / 1h / 15min)
- Proper HA device classes (moisture, battery, voltage)
- LED blink feedback on manual button press
- Soil status text sensor (Normal / Almost Dry / Dry)

**Entities exposed to Home Assistant:**

| Entity | Type | Description |
|--------|------|-------------|
| Soil Moisture | Sensor | Calibrated moisture percentage (0–100%) |
| Soil Status | Text Sensor | Normal / Almost Dry / Dry |
| Battery | Sensor | Battery percentage |
| Battery Voltage | Diagnostic | Raw battery voltage |
| Soil Moisture Raw (V) | Diagnostic | Raw ADC voltage (used for calibration) |

**Calibration:**  
After flashing the initial firmware, you will want to do a calibration for your soil type. Have a pot of dry soil and another of wet soil on hand. Dip sensor into the dry soil, click button, record voltage. You will need to enter this value back into the yaml file under substitutions "dry_voltage: voltage_reading_here" . You will need to do the exact same thing for wet soil and enter the voltage under "wet_voltage: voltage_reading_here" .
Now reflash and you are ready to go.

**Hardware pinout (XIAO ESP32-C6):**

| Pin | Function |
|-----|----------|
| GPIO1 (D1) | Soil probe ADC |
| GPIO0 (D0) | Battery voltage ADC |
| GPIO21 (D3) | 200kHz PWM capacitive excitation |
| GPIO14 | Sensor power / boost converter enable |
| GPIO3 | Keep LOW on boot |
| GPIO18 (D10) | Yellow LED — Almost Dry |
| GPIO19 (D8) | Green LED — Normal |
| GPIO20 (D9) | Red LED — Dry |
| GPIO2 (D2) | Button / deep sleep wake pin |

**Notes:**
- Requires `secrets.yaml` with `wifi_ssid`, `wifi_password`, `api_encryption_key`, `ota_password`, and `ap_password` or you can simply fill those parameters directly in the yaml file.
- First boot will broadcast an AP for WiFi setup — connect and configure via captive portal.
- ESPHome 2026.5.1+ required — earlier versions have a broken ADC component for ESP32-C6 with ESP-IDF 5.3.x

---

## Secrets

All sensitive values are stored in `secrets.yaml` which is excluded from this repo via `.gitignore`. Required keys:

```yaml
wifi_ssid: ""
wifi_password: ""
api_encryption_key: ""
ota_password: ""
ap_password: ""
```

---

## License

MIT
