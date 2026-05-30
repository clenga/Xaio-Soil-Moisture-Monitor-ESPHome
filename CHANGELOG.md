# Changelog

## v2 - 2026-05-26
### Changed
- Updated dry_voltage and wet_voltage calibrated for coco/perlite mix
- Fixed battery multiply from 2.0 to 1.0 (no voltage divider on this board)
- Fixed battery percentage curve top end from 1.6V to 1.5V
- Fixed Soil Status text sensor staying Unknown
- Redacted credentials, moved to secrets.yaml

## v1 - 2026-05-26
### Initial release
- Real moisture percentage (0-100%) via calibrated ADC
- Raw voltage diagnostic sensor for calibration
- Battery voltage and percentage entities
- Adaptive deep sleep (8h / 1h / 15min)
- LED blink feedback on button press
- Soil Status text sensor (Normal / Almost Dry / Dry)
