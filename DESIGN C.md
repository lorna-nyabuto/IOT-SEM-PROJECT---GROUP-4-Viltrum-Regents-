# Design C: ESP32 + DHT22 + Relay connected to ESP32 + MQ-5

## Objective
To control a relay based on environmental conditions while monitoring gas levels using a second ESP32.

## Components
- ESP32 #1
- DHT22 Sensor
- Relay Module
- ESP32 #2
- MQ-5 Sensor

## Schematic Diagram

![Design C](design_c.png)

## Description
ESP32 #1 monitors temperature and humidity and controls the relay. ESP32 #2 monitors gas concentration using the MQ-5 sensor.
