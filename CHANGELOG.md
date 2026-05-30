# Changelog

## v2.1 - 2026-05-29
### Changed
- Recalibrated dry_voltage from 2.50 to 2.35 (tuned for coco/perlite mix)
- Recalibrated wet_voltage from 1.342 to 1.775 (tuned for coco/perlite mix)
- Note: coco/perlite retains less moisture than pure coco coir, resulting
  in a higher wet voltage reading compared to water calibration

## v2.0 - 2026-05-26
### Changed
- Updated dry_voltage from 2.80 to 2.50 (adjusted from open-air default)
- Updated wet_voltage from 1.20 to 1.342 (measured in water)
- Fixed battery multiply from 2.0 to 1.0 (no voltage divider on this board)
- Fixed battery percentage curve top end from 1.6V to 1.5V (AA nominal)
- Fixed Soil Status text sensor staying Unknown (added component.update call)
- Moved all credentials to secrets.yaml

## v1.0 - 2026-05-26
### Initial release
- Real moisture percentage (0-100%) via calibrated ADC
- Raw voltage diagnostic sensor for calibration
- Battery voltage and percentage entities
- Adaptive deep sleep (8h / 1h / 15min)
- LED blink feedback on button press
- Soil Status text sensor (Normal / Almost Dry / Dry)
