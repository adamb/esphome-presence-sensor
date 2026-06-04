# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is an **ESPHome** project for an ESP32-based device named "office". ESPHome is a framework for building smart home devices that integrate with Home Assistant. The project uses the ESP-IDF framework and communicates via the Home Assistant API with OTA (Over-The-Air) update support.

## Key Files & Configuration

- **`first.yaml`** - Main ESPHome device configuration. Defines the device name ("office"), board type (ESP32), WiFi settings, Home Assistant API encryption, and enabled features (logging, OTA, captive portal).
- **`.esphome/`** - ESPHome build directory (auto-generated, can be deleted and rebuilt).

## Common Commands

### Validate Configuration
```bash
esphome config first.yaml
```
Validates the YAML configuration without building.

### Build Firmware
```bash
esphome compile first.yaml
```
Compiles the firmware. Output is in `.esphome/build/office/`.

### Flash Device (USB)
```bash
esphome run first.yaml
```
Builds and flashes the device over USB. Interactive—follow prompts to select the serial port.

### Upload Over-The-Air (OTA)
```bash
esphome upload first.yaml
```
Uploads firmware to the device over WiFi (requires device to be running and connected).

### Monitor Serial Output
```bash
esphome logs first.yaml
```
Opens a serial monitor to view device logs in real-time.

### Clean Build
```bash
rm -rf .esphome/build
```
Then run `esphome compile first.yaml` to rebuild from scratch.

## ESPHome Configuration Syntax

The YAML files use ESPHome's domain-specific configuration language. Key sections in the current config:

- **`esphome:`** - Device metadata (name, etc.)
- **`esp32:`** - Board configuration (board type, framework)
- **`logger:`** - Enable serial logging
- **`api:`** - Home Assistant API integration with encryption
- **`ota:`** - Over-The-Air update platform
- **`wifi:`** - WiFi credentials and fallback hotspot
- **`captive_portal:`** - Fallback web portal if WiFi fails

## Architecture Notes

- **No custom components**: Currently using only built-in ESPHome components.
- **Single device config**: The project has one device configuration file. If adding multiple devices in the future, create separate YAML files per device (e.g., `living_room.yaml`, `bedroom.yaml`).
- **Home Assistant integration**: The device integrates via the native API. Ensure the Home Assistant instance has the correct encryption key to pair with the device.

## Development Workflow

1. **Edit** `first.yaml` to add sensors, switches, or other components.
2. **Validate** with `esphome config first.yaml` to catch syntax errors early.
3. **Build** locally: `esphome compile first.yaml` to verify compilation.
4. **Deploy**:
   - First time: `esphome run first.yaml` (USB) to flash initial firmware.
   - Subsequent updates: `esphome upload first.yaml` (OTA) or `esphome run first.yaml` (USB).
5. **Monitor** with `esphome logs first.yaml` to debug issues.

## Useful References

- [ESPHome Documentation](https://esphome.io/) - Full component and configuration reference
- [Home Assistant Integration](https://esphome.io/components/api.html) - Details on the API component
- [ESP-IDF Framework](https://docs.espressif.com/projects/esp-idf/en/stable/esp32/) - Low-level framework documentation
