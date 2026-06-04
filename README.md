# ESPHome Presence Sensor

ESP32-based presence detection using the LD2410C mmWave radar sensor. Integrates with Home Assistant via the native ESPHome API.

## Hardware

- ESP32 NodeMCU Dev Board v1.1 (or compatible ESP32)
- LD2410C mmWave presence sensor

### Wiring

| ESP32 | LD2410C |
|-------|---------|
| GPIO18 (TX) | RX |
| GPIO19 (RX) | TX |
| 5V | VCC |
| GND | GND |

> **Note:** GPIO16/17 didn't work on NodeMCU ESP32 Dev Board v1.1. GPIO18/19 are reliable UART pins. Use 5V for stable operation.

## Setup

1. Copy `secrets.yaml.example` to `secrets.yaml` and fill in your credentials:

```yaml
wifi_ssid: "your-wifi-ssid"
wifi_password: "your-wifi-password"
api_key: "your-32-character-base64-key"
fallback_password: "fallback-hotspot-password"
```

2. Generate an API key:
```bash
python3 -c "import secrets; print(base64.b64encode(secrets.token_bytes(32)).decode())"
```

3. Flash the device:
```bash
esphome run presence-sensor.yaml
```

## Home Assistant Integration

The device automatically appears in Home Assistant when discovered on your network. Add it via Settings → Devices → Add Device, then enter the API encryption key when prompted.

## Sensors

- **Presence detected** - Binary sensor, true when human presence detected
- **Moving target** - Binary sensor for motion detection
- **Still target** - Binary sensor for stationary presence
- **Moving/Still distance** - Distance to target in cm
- **Moving/Still energy** - Signal strength indicators

## OTA Updates

After initial USB flash, update over WiFi:
```bash
esphome upload presence-sensor.yaml
```

## License

MIT