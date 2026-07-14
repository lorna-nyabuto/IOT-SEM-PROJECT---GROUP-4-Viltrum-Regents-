ICS 4111 [Apr-Jul 2026] Semester Project: Deliverable 1 || Page 1

# ICS 4111: Embedded Systems & IoT
## Semester Project: Deliverable 1 — Group 4 (Viltrum Regents)
### Flora Farms Greenhouse Monitoring System
### Flower: Daisy (Gerbera)

### Members
* Lorna Nyabuto — 142544
* Wesley Mutisya — 132989
* Jeremy Chege — 148654
* Bill Otieno — 163362
* Trevor James — 167612
* Nicole Kirimi — 147585

---

### Question 1: Environmental Growth Requirements

#### 1. Optimal Temperature Range
The Gerbera Daisy is a warm-season crop that needs a consistent but moderate thermal range. In daytime, optimum temperature is 22–25 °C. At night, temperatures drop to 12–15 °C. An overall optimum temperature is near 23 °C (Agriculture.Institute, 2025; DryGair Energies, 2023).

#### 2. Optimal Relative Humidity Range
Gerbera Daisies originate from naturally humid environments, and thrive best at relative humidity between 70% and 80% (Agriculture.Institute, 2025; JayNarayanTiwari3, n.d.). Adequate humidity supports bloom quality, but excessive humidity encourages powdery mildew and Botrytis, which are leading causes of crop loss in gerbera daisies (Greenhouse Grower, 2019).

#### 3. Recommended Soil Type
Commercial gerbera daisies require porous, well-drained, fertile soil rich in organic matter. The most widely cited industry mix is **coarse peat moss combined with approximately 20% perlite**, which balances water retention with the aeration that gerbera roots require (Greenhouse Grower, 2019).

Equivalent formulations using one-third sand, one-third leaf-mould/peat and one-third rich loam are also documented (Miller Horticultural Library, University of Washington Botanic Gardens, n.d.). Soils that hold excess water cause crown and root rot, the single most damaging cultural failure in gerbera production (Stauffers of Kissel Hill, 2025).

#### 4. Optimal Soil Moisture Content
Gerbera requires consistent but never saturated moisture. Practical irrigation guidance is to allow the topsoil to dry slightly between watering and to deliver approximately **25 mm (1 inch) of water per week**, typically as deep, infrequent applications rather than shallow daily passes (Adams Fairacre Farms, 2023).

A working target band is approximately 25–35% VWC (Volumetric Water Content). Dropping below 20% causes wilt and bud abortion, while values above 40% risk crown rot (Adams Fairacre Farms, 2023; Greenhouse Grower, 2019). Overhead watering should be avoided to keep foliage dry (Katherine Rowe, 2025).

#### 5. Optimal Soil pH Range
Gerbera daisies thrive in mildly acidic soil. The commercial optimum soil pH is 5.5–5.8, with a broader tolerable range of 5.5–6.5 (Greenhouse Grower, 2019; Miller Horticultural Library, University of Washington Botanic Gardens, n.d.; Stauffers of Kissel Hill, 2025). Continuous pH monitoring is as important as initial soil preparation because pH drifts over time with fertilization and irrigation.

#### 6. Suitable Sunlight Exposure
Gerbera is a full-sun species requiring **6–8 hours of direct sunlight per day** for prolific flowering, with bright morning sun preferred over harsh afternoon light (Gardenia.net, 2026; Katherine Rowe, 2025). In greenhouse terms this corresponds to a canopy-level light intensity of approximately **450–600 foot-candles** (JayNarayanTiwari3, n.d.). Insufficient light produces weak, leggy stems and reduced bloom count, while uncontrolled midday sun in hot conditions causes leaf scorch and petal fade, justifying shade-cloth management above ~27 °C (Agriculture.Institute, 2025).

#### Summary Table

| Parameter | Optimal Range | Critical Thresholds |
|---|---|---|
| Temperature | Daytime: 22–25 °C<br>Nighttime: 12–15 °C<br>Overall optimum: 23 °C | < 12 °C or > 35 °C halts bud initiation<br>> 27 °C causes heat stress |
| Relative Humidity | 70–80% | > 85% invites Botrytis and powdery mildew |
| Soil Type | Porous, well-drained, high organic matter (peat moss + 20% perlite) | Waterlogged soils cause crown rot |
| Soil Moisture | Approx. 25–35% VWC<br>~25 mm water per week | < 20% VWC wilt<br>> 40% VWC root/crown rot |
| Soil pH | 5.5–5.8 optimum (5.5–6.5 acceptable) | < 5.5 leaf spotting<br>≥ 6.5 Iron/Magnesium deficiency |
| Sunlight | 6–8 hours direct sun per day (≈ 450–600 fc canopy intensity) | < 4 h reduces blooming<br>midday > 27 °C requires shade |

#### References
* Adams Fairacre Farms. (2023, April 15). *Gerbera Daisies Info & Care*. Adams Fairacre Farms – Garden Tips. adamsfarms.com/gardentips/gerbera-daisies-info-care/
* Agriculture.Institute. (2025, October 30). *Gerbera: Cultivation and Care in Greenhouse Conditions*. Agriculture Notes by Agriculture.Institute. agriculture.institute/floriculture-and-landscaping/gerbera-cultivation-care-greenhouse/
* DryGair Energies. (2023, December 28). How to Grow Gerberas – Gerbera Greenhouse Guide. *DryGair*. drygair.com/blog/gerbera-greenhouse/
* Gardenia.net. (2026, February 18). *Gerbera Daisy – All You Need to Know*. Gardenia. https://www.gardenia.net/plant/gerbera-jamesonii
* Greenhouse Grower. (2019, September 25). *Tips For Producing Gerberas*. Greenhouse Grower. greenhousegrower.com/production/plant-culture/blooming-potted-production/tips-for-producing-gerberas/
* JayNarayanTiwari3. (n.d.). *Greenhouse Cultivation of Gerbera*. Retrieved from slideshare.net/slideshow/gerbera-cultivation-in-poly-house-pptx/283000894
* Katherine Rowe. (2025, June 28). *How to Grow Gerbera Daisies in Pots and Containers*. Epic Gardening. epicgardening.com/gerbera-daisies-pots/
* Miller Horticultural Library, University of Washington Botanic Gardens. (n.d.). *Wilting Gerbera Daisies*. UW Botanic Gardens – Plant Answer Line. Retrieved from depts.washington.edu/hortlib/?p=2924
* Stauffers of Kissel Hill. (2025, January 30). *A Guide to Gerbera Daisy Care*. Stauffers of Kissel Hill. skh.com/blog/a-guide-to-gerbera-daisy-care/

---

### Question 2: Hardware Components

This section lists every hardware component required to build the embedded system, covering all six environmental parameters from Question 1, LPG sensing, on-device display, local control, and prototyping infrastructure.

#### 2.1 Microcontroller and Communications
The system's central microcontroller is the **ESP32-S DevKit (30-pin)**. It integrates a dual-core processor, 4 MB flash, and built-in Bluetooth/Wi-Fi radios, allowing direct connection to the greenhouse Wi-Fi network for cloud uplink without a separate communications module.

#### 2.2 Local Display
A **1.3" 128×64 IIC OLED display** (SH1106 driver) provides an on-device readout for live sensor values during commissioning and serves as a fallback indicator if Wi-Fi connectivity is lost. Its I²C interface allows it to share a two-wire bus with other digital sensors, conserving GPIOs.

#### 2.3 Environmental Sensors
The six parameters from the Question 1 table are covered by the following sensors. Soil type is determined once during media preparation and does not require continuous sensing.

| Parameter | Sensor |
|---|---|
| Temperature | DHT22 / AM2302 (digital) |
| Relative Humidity | DHT22 / AM2302 (digital) |
| Soil Type | Determined once during media prep — no sensor required |
| Soil Moisture | Capacitive soil moisture sensor (analog, via ESP32 ADC) |
| Soil pH | Analog soil pH sensor probe |
| Sunlight | Photoresistor / LDR or lux sensor module (analog or I²C) |

> *Note: soil moisture, soil pH, and light sensing modules are not detailed further in this deliverable's schematic designs, which focus on the gas, temperature/humidity, and display subsystem.*

#### 2.4 LPG Gas Sensing
The **MQ-5** tin-dioxide (SnO₂) semiconductor gas sensor provides analog detection of LPG, natural gas, methane, butane, and propane — the gases relevant to the greenhouse's LPG heating system. Its 5 V heater requires warm-up time (≈24–48 hours initial burn-in, ≈3 minutes per cold start) and its 0–5 V analog output requires a resistor divider before connecting to the ESP32's 3.3 V-tolerant ADC.

#### 2.5 Control / Actuation
A **5 V 1-channel low-level-trigger relay module** (built around the Songle SRD-05VDC-SL-C relay) provides isolated switching of high-current loads such as ventilation fans or solenoid valves, and serves to gate power between two ESP32 nodes. The module includes an on-board optocoupler, transistor driver, and flyback diode, so it can be driven directly from a single ESP32 GPIO.

#### 2.6 Passive Components

| Component | Purpose |
|---|---|
| 10 kΩ resistor | Holds the DHT22's single data wire at 3.3 V when idle, giving the ESP32 a stable line to read instead of random electrical noise. |
| 10 kΩ resistor | Upper resistor of a voltage divider that protects the ESP32 from the MQ-5's 5 V output (works as a pair with the 20 kΩ below). |
| 20 kΩ resistor | Lower resistor of the same divider — the 10:20 ratio scales the MQ-5's 0–5 V output down to ≈0–3.3 V, the highest voltage the ESP32 ADC pin can safely read. |
| 4.7 kΩ resistor | Holds the I²C bus lines (SDA and SCL) high by default so the OLED and light sensor can communicate with the ESP32. Skip these if your modules already have them built onto the PCB. |
| 0.1 µF ceramic capacitor | One per chip, placed right next to its power pin. Acts like a tiny local battery, releasing stored charge to cover sudden current spikes (e.g. when the Wi-Fi radio switches on) and preventing voltage dips that would crash the chip. |
| 10 µF ceramic capacitor | Smooths out larger, slower current surges on the main 5 V supply line — especially when the MQ-5 heater powers up and pulls ~150 mA. |

#### 2.7 Power Supply
For prototyping, the ESP32-S is powered through its Micro-USB connector. For greenhouse deployment, a 5 V / 2 A regulated supply derived from the existing 12 V battery bank via a DC-DC buck converter is suitable.

| Component | Purpose |
|---|---|
| 5 V / 2 A regulated USB or DC supply | Powers ESP32, MQ-5 heater, relay coil |
| USB-A to Micro-USB cable | Programming and bench power |
| LM2596 DC-DC buck converter (deployment only) | Steps the greenhouse 12 V battery rail down to 5 V |

#### 2.8 Prototyping Tools

| Tool | Purpose |
|---|---|
| Half-size or full-size solderless breadboard (≈840 tie points) | Component layout during prototyping |
| Jumper wire set (M–M, M–F, F–F, ≥40 each) | Inter-component wiring |
| Digital multimeter | Voltage, current, and continuity checks |
| Soldering iron + lead-free solder | Attaching pin headers to bare modules |
| USB-A to Micro-USB cable | ESP32 programming and serial debug |
| Laptop with Arduino IDE / PlatformIO / ESP-IDF | Firmware development and flashing |

---

### Question 3: Datasheets

Datasheet links for each of the five specified components are provided below. Where the listed component is a generic module rather than a chip, the datasheet of the controller IC the module is built around is cited, since that document defines its electrical behaviour, alongside a module-level reference for pinout and wiring.

#### 3.1 — 1.3" White IIC 128×64 OLED LCD
Built around the **Sino Wealth / Univision SH1106** OLED driver IC. Supports I²C and SPI interfaces and operates from 3.3–5 V.
* **Driver IC datasheet (Univision SH1106):** https://www.pololu.com/file/0J1813/SH1106.pdf
* **Module-level datasheet (SparkFun-hosted):** https://cdn.sparkfun.com/assets/2/6/8/9/7/1.3inch-SH1106-OLED_Datasheet.pdf
* **Waveshare user manual (pinout and wiring reference):** https://www.waveshare.com/w/upload/7/76/1.3inch_OLED_UserManual.pdf

#### 3.2 — ESP32-S DevKit Wi-Fi + BLE Module (30-pin)
Built around the **Espressif ESP32-WROOM-32** module, which integrates the ESP32-D0WDQ6 SoC.
* **ESP32-WROOM-32 module datasheet (Espressif, official):** https://www.espressif.com/sites/default/files/documentation/esp32-wroom-32_datasheet_en.pdf
* **ESP32-WROOM-32D / 32U datasheet (revision used on most modern 30-pin DevKits):** https://www.espressif.com/sites/default/files/documentation/esp32-wroom-32d_esp32-wroom-32u_datasheet_en.pdf
* **ESP32 series datasheet (underlying SoC):** https://www.espressif.com/sites/default/files/documentation/esp32_datasheet_en.pdf

#### 3.3 — DHT22 / AM2302 Temperature and Humidity Sensor
Manufactured by **Aosong (Guangzhou) Electronics**, sold under the alternate name AM2302 when supplied with a connecting wire. Outputs calibrated digital readings over a single-wire bus, operating from 3.3–6 V.
* **DHT22 datasheet (Aosong, hosted by SparkFun):** https://cdn.sparkfun.com/assets/f/7/d/9/c/DHT22.pdf
* **AM2302 product manual (Aosong, hosted by Adafruit):** https://cdn-shop.adafruit.com/datasheets/Digital+humidity+and+temperature+sensor+AM2302.pdf

#### 3.4 — MQ-5 LPG / Natural Gas / Coal Gas Sensor
A tin-dioxide (SnO₂) semiconductor gas sensor with high sensitivity to LPG, natural gas, town gas, methane, butane, and propane. Manufactured by **Hanwei Electronics** and second-sourced by **Winsen Electronics**.
* **MQ-5 technical datasheet (Hanwei, hosted by Seeed Studio):** https://files.seeedstudio.com/wiki/Grove-Gas_Sensor-MQ5/res/MQ-5.pdf
* **MQ-5 manual v1.5 (Winsen, official):** https://www.winsen-sensor.com/d/files/MQ-5.pdf

#### 3.5 — 5 V 1-Channel Low-Level-Trigger Relay Module
Built around the **Ningbo Songle SRD-05VDC-SL-C** electromechanical relay, rated for up to 10 A at 250 VAC / 30 VDC. Adds an optocoupler for input isolation, a transistor driver, an LED status indicator, and a flyback diode on the relay coil.
* **SRD-05VDC-SL-C relay datasheet (Songle, hosted by Circuit Basics):** https://www.circuitbasics.com/wp-content/uploads/2015/11/SRD-05VDC-SL-C-Datasheet.pdf
* **SRD-05VDC-SL-C datasheet (Songle, via AllDatasheet):** https://www.alldatasheet.com/datasheet-pdf/pdf/1132639/SONGLERELAY/SRD-05VDC-SL-C.html

---

### Question 4: Schematic Designs

#### Design A: ESP32 + MQ-5 + DHT22 + LCD

**Objective:** To monitor gas concentration, temperature, and humidity using a single ESP32 and display the readings on an LCD.

**Components:**
* 1 ESP32S
* 1 MQ-5 Gas Sensor
* 1 DHT22 Sensor
* 1 LCD Display

**Schematic Diagram:**

<img width="745" height="450" alt="image" src="https://github.com/user-attachments/assets/21a1c045-d79a-4006-92e7-4fbb94c76b3d" />


**Description:** The ESP32 reads data from the MQ-5 and DHT22 sensors and displays the values on the LCD.

**Connections:**
* MQ-5 AOUT → ESP32 GPIO34
* DHT22 DATA → ESP32 GPIO4
* LCD SDA → ESP32 GPIO21
* LCD SCL → ESP32 GPIO22

---

#### Design B: ESP32 + MQ-5 communicating with ESP32 + DHT22

**Objective:** To separate gas sensing and environmental sensing across two ESP32 boards.

**Components:**
* ESP32 #1
* MQ-5 Sensor
* ESP32 #2
* DHT22 Sensor

**Schematic Diagram:**

<img width="798" height="424" alt="image" src="https://github.com/user-attachments/assets/81553029-7939-42e1-b21f-ad5dadd1f650" />


**Description:** ESP32 #1 reads gas levels from the MQ-5 and communicates with ESP32 #2, which reads temperature and humidity from the DHT22.

---

#### Design C: ESP32 + DHT22 + Relay connected to ESP32 + MQ-5

**Objective:** To control a relay based on environmental conditions while monitoring gas levels using a second ESP32.

**Components:**
* ESP32 #1
* DHT22 Sensor
* Relay Module
* ESP32 #2
* MQ-5 Sensor

**Schematic Diagram:**

<img width="894" height="481" alt="image" src="https://github.com/user-attachments/assets/500c470d-14c5-4b6c-a385-edbbf39b635f" />


**Description:** ESP32 #1 monitors temperature and humidity and controls the relay. ESP32 #2 monitors gas concentration using the MQ-5 sensor.

---

### Evidence of Groupwork

*[To be added — group meeting photos / notes for Deliverable 1 have not been provided yet.]*
