Design B: ESP32 + MQ-5 communicating with ESP32 + DHT22

## Objective
To separate gas sensing and environmental sensing across two ESP32 boards.

## Components
- ESP32 #1
- MQ-5 Sensor
- ESP32 #2
- DHT22 Sensor

## Schematic Diagram

![Design B](design_b.png)

## Description
ESP32 #1 reads gas levels from the MQ-5 and communicates with ESP32 #2, which reads temperature and humidity from the DHT22.
