**ICS 4111 – EMBEDDED SYSTEMS AND IoT**

**Semester Project: Deliverable 1**

**Group 4: Viltrum Regents**

**Flora Farms Greenhouse Monitoring Stem**

**Flower: Daisy (Gerbera)**

**Question 2: Hardware Components**

This section lists every hardware component required to build the embedded system. This component list covers all six environmental parameters from question 1. It also covers the LPG sensing, the on-device display, local control, and prototyping infrastructure.

**2.1 Microcontroller and Communications**

The system’s central microcontroller will be the ESP32-S DevKit(30-pin_. It integrates a dual-core processor, 4 MB flash, and built-in Bluetooth/Wi-Fi radios, allowing for direct connection to the greenhouse Wi-Fi network for cloud uplink without a separate module for communication

**2.2 Local Display**

A **1.3" 128 × 64 IIC OLED display** (SH1106 driver) provides an on-device readout for live sensor values during commissioning and serves as a fallback indicator if Wi-Fi connectivity is lost. Its I²C interface allows it to share a two-wire bus with other digital sensors, conserving GPIOs (General Purpose Input/Output).

**2.3 Environmental Sensors**

The six parameters in the Question 1 table are covered by the following sensors. Soil type is determined once during media preparation and does not require continuous sensing.

INSERT PARAM TABLE

**2.4 LPG Gas sensing**

The **MQ-5** tin-dioxide (SnO₂) semiconductor gas sensor provides analog detection of LPG, natural gas, methane, butane, and propane, which are the gases relevant to the greenhouse's LPG heating system. Its 5 V heater requires warm-up time (≈ 24–48 hours initial burn-in, ≈ 3 minutes per cold start) and its 0–5 V analog output requires a resistor divider before connecting to the ESP32's 3.3 V-tolerant ADC.

**2.5 Control/Actuation**

A **5 V 1-channel low-level-trigger relay module** (built around the Songle SRD-05VDC-SL-C relay) provides isolated switching of high-current loads such as ventilation fans or solenoid valves, and serves to gate power between two ESP32 nodes. The module includes an on-board optocoupler, transistor driver, and flyback diode, so it can be driven directly from a single ESP32 GPIO.

**2.6 Passive Components**

|     |     |
| --- | --- |
| COMPONENT | PURPOSE |
| 10 kΩ resistor | Holds the DHT22's single data wire at 3.3 V when idle, giving the ESP32 a stable line to read instead of random electrical noise. |
| 10 kΩ resistor | Upper resistor of a voltage divider that protects the ESP32 from the MQ-5's 5 V output (works as a pair with the 20 kΩ below). |
| 20 kΩ resistor | Lower resistor of the same divider — the 10 : 20 ratio scales the MQ-5's 0–5 V output down to ≈ 0–3.3 V, the highest voltage the ESP32 ADC pin can safely read. |
| 4.7 kΩ resistor | Hold the I²C bus lines (SDA and SCL) high by default so the OLED and light sensor can communicate with the ESP32. Skip these if your modules already have them built onto the PCB. |
| 0.1 µF ceramic capacitor | One per chip, placed right next to its power pin. Acts like a tiny local battery, releasing stored charge to cover sudden current spikes (e.g. when the Wi-Fi radio switches on) and preventing voltage dips that would crash the chip. |
| 10 µF ceramic capacitor | Smooths out larger, slower current surges on the main 5 V supply line — especially when the MQ-5 heater powers up and pulls ~150 mA. |

**2.7 Power Supply**

For prototyping, the ESP32-S is powered through its Micro-USB connector. For greenhouse deployment, a 5 V / 2 A regulated supply derived from the existing 12 V battery bank via a DC-DC buck converter is suitable.

|     |     |
| --- | --- |
| **Component** | **Purpose** |
| 5 V / 2 A regulated USB or DC supply | Powers ESP32, MQ-5 heater, relay coil |
| USB-A to Micro-USB cable | Programming and bench power |
| LM2596 DC-DC buck converter (deployment only) | Steps the greenhouse 12 V battery rail down to 5 V |

**2.8 Prototyping Tools**

|     |     |
| --- | --- |
| **Tool** | Purpose |
| Half-size or full-size solderless breadboard (≈ 840 tie points) | Component layout during prototyping |
| Jumper wire set (M–M, M–F, F–F, ≥ 40 each) | Inter-component wiring |
| Digital multimeter | Voltage, current, and continuity checks |
| Soldering iron + lead-free solder | Attaching pin headers to bare modules |
| USB-A to Micro-USB cable | ESP32 programming and serial debug |
| Laptop with Arduino IDE / PlatformIO / ESP-IDF | Firmware development and flashing |