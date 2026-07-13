ICS 4111 [Apr-Jul 2026] Semester Project: Deliverable 3 || Page 1

# ICS 4111: Embedded Systems & IoT
## Semester Project: Deliverable 3 — Group 4 (Viltrum Regents)
### Flora Farms Greenhouse Monitor (Gerbera daisy cultivation)

### Members
* Lorna Nyabuto — 142544
* Wesley Mutisya — 132989
* Jeremy Chege — 148654
* Bill Otieno — 163362
* Trevor James — 167612
* Nicole Kirimi — 147585

---

### 1. Objective

Transmit and visualise greenhouse sensor data (temperature, humidity, gas levels) on cloud platforms, building on the hardware architecture established in Deliverables 1 and 2.

---

### 2. Device Architecture

* **Microcontroller:** ESP32-S
* **Temperature/Humidity sensor:** DHT22 (GPIO15, 10kΩ pull-up resistor to 3.3V)
* **Gas sensor:** MQ-5, simulated using Wokwi's `wokwi-gas-sensor` part, which models an MQ2-class sensor with an identical analog interface (VCC, GND, AOUT). This substitution was necessary because Wokwi does not provide an exact MQ-5 part. The MQ-5 and MQ2 share the same electrical characteristics (5V supply, single analog output), so the simulated readings and wiring are representative of the physical MQ-5 setup used in earlier deliverables.
* **Display:** 16x2 I2C LCD (address 0x27)

---

### 3. Prototype Submission Link

**Simulation Link:** https://wokwi.com/projects/469367865154757633

The full system was simulated on Wokwi, including sensor readings displayed locally on the LCD and pushed to InfluxDB Cloud over WiFi every 10 seconds.

---

### 4. Embedded & Cloud Communication Codebase

#### ESP32 Cloud-Connected Node Code Script (`sketch.ino`)
```cpp
#include <Wire.h>
#include <LiquidCrystal_I2C.h>
#include <DHT.h>
#include <WiFi.h>
#include <WiFiClientSecure.h>
#include <HTTPClient.h>

//PIN DEFINITIONS
#define DHTPIN 15
#define DHTTYPE DHT22
#define MQ_PIN 34

//OBJECTS
DHT dht(DHTPIN, DHTTYPE);
LiquidCrystal_I2C lcd(0x27, 16, 2);  // Address 0x27, 16x2 LCD

//WiFi CREDENTIALS 
const char* ssid = "Wokwi-GUEST";
const char* password = "";

// InfluxDB Cloud credentials
const char* INFLUX_URL    = "https://us-east-1-1.aws.cloud2.influxdata.com/api/v2/write";
const char* INFLUX_ORG    = "ViltrumRegents";
const char* INFLUX_BUCKET = "greenhouse_data";
const char* INFLUX_TOKEN  = "<YOUR_INFLUXDB_TOKEN_HERE>";

unsigned long lastSend = 0;
const unsigned long SEND_INTERVAL = 10000; // push every 10s

void connectWiFi() {
  WiFi.begin(ssid, password);
  Serial.print("Connecting to WiFi");
  lcd.setCursor(0, 0);
  lcd.print("Connecting WiFi");
  while (WiFi.status() != WL_CONNECTED) {
    delay(500);
    Serial.print(".");
  }
  Serial.println(" Connected!");
  Serial.print("IP Address: ");
  Serial.println(WiFi.localIP());
  lcd.clear();
}

void sendToInflux(float temperature, float humidity, int gasValue) {
  if (WiFi.status() != WL_CONNECTED) return;

  WiFiClientSecure client;
  client.setInsecure(); 

  HTTPClient http;
  String url = String(INFLUX_URL) + "?org=" + INFLUX_ORG + "&bucket=" + INFLUX_BUCKET + "&precision=s";

  http.begin(client, url);
  http.addHeader("Authorization", String("Token ") + INFLUX_TOKEN);
  http.addHeader("Content-Type", "text/plain; charset=utf-8");

  // Line protocol: measurement,tag=value field=value,field=value
  String payload = "greenhouse,device=esp32_s1 temperature=" + String(temperature, 1) +
                    ",humidity=" + String(humidity, 1) +
                    ",gas_raw=" + String(gasValue);

  int httpCode = http.POST(payload);
  Serial.print("InfluxDB write status: ");
  Serial.println(httpCode);
  http.end();
}

void setup() {
  Serial.begin(115200);

  // Initialize DHT22
  dht.begin();

  // Initialize LCD
  lcd.init();
  lcd.backlight();
  lcd.setCursor(0, 0);
  lcd.print("System Ready!");
  delay(1000);
  lcd.clear();

  // Connect to WiFi
  connectWiFi();
}

void loop() {
  // Read DHT22 sensor
  float temperature = dht.readTemperature();
  float humidity = dht.readHumidity();

  // Read gas sensor
  int gasValue = analogRead(MQ_PIN);

  // Check if readings are valid
  if (isnan(temperature) || isnan(humidity)) {
    Serial.println("Failed to read from DHT22!");
    lcd.setCursor(0, 0);
    lcd.print("Sensor Error!  ");
    delay(2000);
    return;
  }

  // Print to Serial Monitor
  Serial.print("Temp: ");
  Serial.print(temperature);
  Serial.print("C, Humidity: ");
  Serial.print(humidity);
  Serial.print("%, Gas: ");
  Serial.println(gasValue);

  // Display on LCD
  lcd.setCursor(0, 0);
  lcd.print("T:");
  lcd.print(temperature, 1);
  lcd.print("C H:");
  lcd.print(humidity, 1);
  lcd.print("%  ");

  lcd.setCursor(0, 1);
  lcd.print("Gas:");
  lcd.print(gasValue);
  lcd.print("    ");

  // Push to InfluxDB every SEND_INTERVAL
  if (millis() - lastSend > SEND_INTERVAL) {
    lastSend = millis();
    sendToInflux(temperature, humidity, gasValue);
  }

  delay(2000);
}
```

**Required Libraries (`libraries.txt`):**
* LiquidCrystal I2C
* DHT sensor library

---

### 5. Part 1: Cloud Data Storage (InfluxDB Cloud)

Sensor readings (`temperature`, `humidity`, `gas_raw`) are written to a time-series bucket in InfluxDB Cloud using the HTTP v2 write API, in line protocol format:

```
greenhouse,device=esp32_s1 temperature=<value>,humidity=<value>,gas_raw=<value>
```

**Organization:** ViltrumRegents
**Bucket:** greenhouse_data

**Evidence:**

<img width="1905" height="886" alt="image" src="https://github.com/user-attachments/assets/2fd93213-c167-4ccd-b622-7ed5b40ad84d" />


*Figure 1: InfluxDB Evidence*

---

### 6. Part 2: Cloud Visualisation (Grafana)

A Grafana dashboard ("Flora Farms Greenhouse Monitor") was built with three time-series panels querying InfluxDB via Flux:

1. Temperature (°C)
2. Humidity (%)
3. Gas Sensor (raw ADC)

**Public Grafana dashboard link:** https://ivorybarracuda1165.grafana.net/public-dashboards/a330f28dc55d4fd58207eead73f2ba41
<img width="975" height="454" alt="image" src="https://github.com/user-attachments/assets/af020b93-20fe-440f-88bd-6346fb1b41e9" />

---

### 7. Engineering Implementation Details & Assumptions

* **MQ-5 Gas Sensor Representation:** Because Wokwi does not provide a native MQ-5 part, the `wokwi-gas-sensor` block (an MQ2-class part) was used instead. It shares the same 5V supply and single analog-output interface as the MQ-5, so wiring and readings remain representative of the physical setup used in Deliverable 2.
* **Cloud Write Cadence:** Sensor data is pushed to InfluxDB every 10 seconds (`SEND_INTERVAL`), independent of the 2-second local LCD/Serial refresh cycle, to avoid flooding the cloud write API while keeping the on-device display responsive.
* **Transport Security:** `WiFiClientSecure::setInsecure()` is used to skip TLS certificate validation for the Wokwi simulation environment; a physical deployment should validate the InfluxDB Cloud certificate instead.

---

### 8. Evidence of Groupwork

The group met in the lab on Thursday, 9th July 2026 and Friday, 10th July 2026 to assemble and test the physical prototype. After encountering an unresolved firmware issue during testing, the group collectively decided to proceed with a Wokwi simulation instead, as permitted by the deliverable instructions. Full details are documented in the meeting minutes (`Meeting_Minutes_Deliverable3.md`).

Below are photos of the group members in the lab:

<img width="899" height="1599" alt="image" src="https://github.com/user-attachments/assets/fcc84acc-efb1-4a83-834c-2aca0b868791" />
<img width="525" height="934" alt="image" src="https://github.com/user-attachments/assets/1fe25260-616f-4aa4-bb7a-178293a502c5" />
<img width="512" height="512" alt="image" src="https://github.com/user-attachments/assets/b6565796-5aae-42b4-9c16-a1e123ca85aa" />
<img width="518" height="518" alt="image" src="https://github.com/user-attachments/assets/15d9c4aa-fa3c-4326-b5ef-e4ce2c5c5451" />

