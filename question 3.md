**ICS 4111 – EMBEDDED SYSTEMS AND IoT**

**Semester Project: Deliverable 1**

**Group 4: Viltrum Regents**

**Flora Farms Greenhouse Monitoring Stem**

**Flower: Daisy (Gerbera)**

**Question 3: Datasheets**

The datasheet links for each of the five specified components are provided below. Where the listed component is a generic module (rather than a chip), I cite the datasheet of the controller IC the module is built around, since that document defines its electrical behaviour. In addition, a module-level reference for pinout and wiring.

**3.1 — 1.3" White IIC 128 × 64 OLED LCD**

The 1.3" white 128 × 64 IIC OLED module is built around the **Sino Wealth / Univision SH1106** OLED driver IC. It supports I²C and SPI interfaces and operates from 3.3–5 V.

- **Driver IC datasheet (Univision SH1106):** https://www.pololu.com/file/0J1813/SH1106.pdf
- **Module-level datasheet (SparkFun-hosted):** https://cdn.sparkfun.com/assets/2/6/8/9/7/1.3inch-SH1106-OLED_Datasheet.pdf
- **Waveshare user manual (pinout and wiring reference):** https://www.waveshare.com/w/upload/7/76/1.3inch_OLED_UserManual.pdf

**3.2 — ESP32-S DevKit Wi-Fi + BLE Module (30-pin)**

The 30-pin ESP32-S DevKit is a development board built around the **Espressif ESP32-WROOM-32** module, which integrates the ESP32-D0WDQ6 SoC. The module datasheet documents the chip, pin assignments, electrical characteristics, and Wi-Fi / Bluetooth specifications.

- **ESP32-WROOM-32 module datasheet (Espressif, official):** https://www.espressif.com/sites/default/files/documentation/esp32-wroom-32_datasheet_en.pdf
- **ESP32-WROOM-32D / 32U datasheet (revision used on most modern 30-pin DevKits):** https://www.espressif.com/sites/default/files/documentation/esp32-wroom-32d_esp32-wroom-32u_datasheet_en.pdf
- **ESP32 series datasheet (underlying SoC):** https://www.espressif.com/sites/default/files/documentation/esp32_datasheet_en.pdf

**3.3 — DHT22 / AM2302 Temperature and Humidity Sensor**

The DHT22 (sold under the alternate name **AM2302** when supplied with a connecting wire) is manufactured by **Aosong (Guangzhou) Electronics**. It outputs calibrated digital readings over a single-wire bus and operates from 3.3–6 V.

- **DHT22 datasheet (Aosong, hosted by SparkFun):** https://cdn.sparkfun.com/assets/f/7/d/9/c/DHT22.pdf
- **AM2302 product manual (Aosong, hosted by Adafruit):** https://cdn-shop.adafruit.com/datasheets/Digital+humidity+and+temperature+sensor+AM2302.pdf

**3.4 — MQ-5 LPG / Natural Gas / Coal Gas Sensor**

The MQ-5 is a tin-dioxide (SnO₂) semiconductor gas sensor with high sensitivity to LPG, natural gas, town gas, methane, butane, and propane. It is manufactured by **Hanwei Electronics** and second-sourced by **Winsen Electronics**.

- **MQ-5 technical datasheet (Hanwei, hosted by Seeed Studio):** https://files.seeedstudio.com/wiki/Grove-Gas_Sensor-MQ5/res/MQ-5.pdf
- **MQ-5 manual v1.5 (Winsen, official):** https://www.winsen-sensor.com/d/files/MQ-5.pdf

**3.5 — 5 V 1-Channel Low-Level-Trigger Relay Module**

The 5 V 1-channel relay module is built around the **Ningbo Songle SRD-05VDC-SL-C** electromechanical relay, rated for up to 10 A at 250 VAC / 30 VDC. The module adds an optocoupler for input isolation, a transistor driver, an LED status indicator, and a flyback diode on the relay coil.

- **SRD-05VDC-SL-C relay datasheet (Songle, hosted by Circuit Basics):** https://www.circuitbasics.com/wp-content/uploads/2015/11/SRD-05VDC-SL-C-Datasheet.pdf
- **SRD-05VDC-SL-C datasheet (Songle, via AllDatasheet):** https://www.alldatasheet.com/datasheet-pdf/pdf/1132639/SONGLERELAY/SRD-05VDC-SL-C.html