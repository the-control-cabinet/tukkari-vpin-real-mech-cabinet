# ESPHome configuration

To add: the live `esp-vpin-sensor.yaml` (ESP32 Virtual Pinball). Before committing:
- `api: encryption: key:`, `wifi:` and the fallback `ap:` password must all be `!secret …` references.
- Never commit `secrets.yaml`.

Structure (see [docs/07](../../docs/07-instrumentation-esp32-and-home-assistant.md)): four Hall-clamp rails (ADC1, 12 dB, 20 ms), per-rail fast/smoothed/peak template sensors, zero-offset globals with zero and reset buttons, a one-wire bus (GPIO7) for the DS18B20, and a Bluetooth proxy.
