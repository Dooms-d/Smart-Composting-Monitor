# Firmware

ESP32 sketch for the compost monitoring node.

Drop your existing Arduino `.ino` file here. It should:

1. Read the DS18B20 core temperature probe and the DHT22 humidity sensor
2. Drive the ventilation fan via the transistor when temperature exceeds threshold
3. Update the local TFT display
4. Emit one JSON line per reading over serial at 115200 baud:
   `{"temp": 48.2, "humi": 61.5, "fan": 1}`

## Libraries

- `OneWire` + `DallasTemperature` — DS18B20
- `DHT sensor library` — DHT22
- `TFT_eSPI` (or your display driver)
- `WiFi` + `HTTPClient` — *pending, for the backend transport*

## Wiring

Document your pin assignments here so the project is reproducible.

| Signal | ESP32 pin |
|---|---|
| DS18B20 data | |
| DHT22 data | |
| Fan gate | |
| TFT CS / DC / RST | |
