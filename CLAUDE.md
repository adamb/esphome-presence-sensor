# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is an **ESPHome presence sensor project** for an ESP32-based device. It uses an LD2410C mmWave radar sensor to detect human presence (both moving and stationary) and integrates with Home Assistant.

## Key Files

- **`presence-sensor.yaml`** - Main ESPHome device configuration with LD2410C sensor setup
- **`secrets.yaml`** - WiFi credentials and API encryption key (not tracked in git)
- **`.esphome/`** - ESPHome build directory (auto-generated, safe to delete and rebuild)

## Hardware

- **Board**: ESP32 Dev Module
- **Sensor**: LD2410C mmWave presence sensor
- **UART Wiring**: GPIO17 (TX) → LD2410C RX, GPIO16 (RX) → LD2410C TX

## Sensors Exposed

| Sensor | Type | Description |
|--------|------|-------------|
| Presence detected | binary_sensor | True when any presence detected |
| Moving target | binary_sensor | True when moving target detected |
| Still target | binary_sensor | True when stationary target detected |
| Moving distance | sensor | Distance to moving target (cm) |
| Still distance | sensor | Distance to stationary target (cm) |
| Moving energy | sensor | Signal strength for moving target |
| Still energy | sensor | Signal strength for stationary target |
| Detection distance | sensor | Overall detection distance |

## Common Commands

```bash
# Validate configuration
esphome config presence-sensor.yaml

# Build firmware
esphome compile presence-sensor.yaml

# Flash via USB (first time)
esphome run presence-sensor.yaml

# Upload OTA (subsequent updates)
esphome upload presence-sensor.yaml

# Monitor serial logs
esphome logs presence-sensor.yaml

# Clean build
rm -rf .esphome/build
```

## Development Workflow

1. Edit `presence-sensor.yaml` to modify sensors, thresholds, or add components
2. Validate: `esphome config presence-sensor.yaml`
3. Build: `esphome compile presence-sensor.yaml`
4. Deploy: `esphome run presence-sensor.yaml` (USB) or `esphome upload presence-sensor.yaml` (OTA)
5. Monitor: `esphome logs presence-sensor.yaml`

## Useful References

- [LD2410 Component Docs](https://esphome.io/components/sensor/ld2410.html)
- [ESPHome Documentation](https://esphome.io/)
- [Home Assistant API Integration](https://esphome.io/components/api.html)