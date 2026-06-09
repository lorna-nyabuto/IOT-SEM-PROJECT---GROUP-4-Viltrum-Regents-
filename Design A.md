Design A: ESP32 + MQ-5 + DHT22 + LCD

## Objective
To monitor gas concentration, temperature, and humidity using a single ESP32 and display the readings on an LCD.

## Components
- 1 ESP32S
- 1 MQ-5 Gas Sensor
- 1 DHT22 Sensor
- 1 LCD Display

Schematic Diagram

![Design A](design_a.png)

Description
The ESP32 reads data from the MQ-5 and DHT22 sensors and displays the values on the LCD.

Connections
- MQ-5 AOUT → ESP32 GPIO34
- DHT22 DATA → ESP32 GPIO4
- LCD SDA → ESP32 GPIO21
- LCD SCL → ESP32 GPIO22
