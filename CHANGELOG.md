# Changelog

## v3.5 - 2026-06-01
### Changed
- Fixed Battery Draining too quickly due to not using "mode: INPUT_PULLUP" for the #Deep Sleep settings./
- Set safe_mode to disabled
- Set run_duration to set interval
- Continued Testing over the next 24hours


## v3.x - 2026-05-30
### Changed
- All sleep intervals unified to 1 hour (Dry, Almost Dry, Too Wet) and 8 hours (Normal)
- Removed `run_duration` from deep_sleep — device sleeps immediately after HA sync
- Battery multiply reset to 1.0 for per-device calibration
- HA sync delay reduced from 5s to 3s

### Battery Optimisations
- Eliminated all automatic LED activity on wake cycles entirely
- LEDs now only activate on physical button press
- WiFi timeout reduced from 30s to 15s
- `fast_connect` skips AP scan on every wake
- Removed `safe_mode` to prevent interference with deep sleep boot cycles

---

## v2.4 - 2026-05-30
### Changed
- Removed all automatic LED blinking from boot/wake cycle
- LEDs now button-press only (no auto blinks at any interval)
- Battery multiply corrected to 1.69 for device 3 (onboard voltage divider compensation)
- Removed `dry_wake_count` global (no longer needed without LED throttle)

---

## v2.3 - 2026-05-29
### Added
- Too Wet state (75-100%) with RED-YLW-RED-YLW blink pattern
- `sleep_too_wet_s` substitution (1 hour)
- `normal_pct` substitution (upper Normal boundary)
- `dry_wake_count` global — throttles Dry-state LED blinks to once per hour
- Long press (3s) physical button triggers device reboot with all-LED confirmation flash
- Restart button entity exposed to HA

### Changed
- Moisture thresholds updated: Dry 0-18%, Almost Dry 18-35%, Normal 35-75%, Too Wet 75-100%
- WiFi timeout reduced from 30s to 15s
- HA sync delay reduced from 5s to 3s
- Dry sleep interval changed from 15 min to 1 hour

---

## v2.2 - 2026-05-27
### Added
- 4-state moisture status: Dry / Almost Dry / Normal / Too Wet
- Distinct LED blink patterns per state

### Changed
- `almost_dry_pct` threshold moved to substitutions
- `normal_pct` added as upper boundary substitution

---

## v2.1 - 2026-05-26
### Fixed
- Soil Status text sensor stuck on "Unknown" — added `component.update: soil_status`
  to `take_reading` script so it updates after moisture percentage is calculated
- Battery `multiply` corrected from 2.0 to 1.0 (no voltage divider on this board)
- Battery percentage curve top end corrected from 1.6V to 1.5V (AA alkaline nominal)
- `attenuation: 11dB` deprecated warning resolved — updated to `12dB`

---

## v2.0 - 2026-05-26
### Initial Enhanced Release
- Real moisture percentage (0-100%) via calibrated ADC
- Raw voltage diagnostic sensor exposed for per-unit calibration
- Battery voltage and battery percentage entities
- Adaptive deep sleep matching stock intervals (8h Normal / 1h Almost Dry / 15min Dry)
- Proper HA device classes (moisture, battery, voltage)
- LED blink feedback on button press
- Soil Status text sensor (Normal / Almost Dry / Dry)
- First-boot AP mode preserved via wifi_ever_connected NVS global
- `fast_connect` enabled to skip AP scan on wake
- Resolved dual ADC pin conflict — moisture % derived via template sensor lambda
- Resolved GPIO2 shared pin conflict between deep_sleep wakeup and binary_sensor
- ESPHome 2026.5.1 required — earlier versions have broken ADC component for
  ESP32-C6 with ESP-IDF 5.3.x

---

## v1.0 - 2026-05-26
### Stock Firmware Baseline
- Factory ESPHome firmware from Seeed Studio
- 3-state moisture status (Dry / Almost Dry / Normal Moisture)
- Onboard calibration via 3x button press sequence
- Adaptive deep sleep (15min / 1hr / 8hr)
- AA battery percentage via voltage lookup
