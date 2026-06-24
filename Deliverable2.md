# ICS 4111: Embedded Systems & IoT
## Semester Project: Deliverable 2 — Group 4 (Viltrum Regents)

### 1. Prototype Submission Links
* **Architecture (a) Simulation Link:** [Click Here to View Architecture A Wokwi Workspace] https://wokwi.com/projects/467705563826906113
* **Architecture (b) Uploaded pictures------
* **Architecture (c) Simulation Link:** [Click Here to View Architecture C Wokwi Workspace] https://wokwi.com/projects/467707618590516225
---

### 2. Embedded Simulation Codebase

#### Architecture (a) Code Script (`sketch.ino`)
```cpp
#include <Wire.h>
#include <LiquidCrystal_I2C.h>
#include <DHT.h>

// Microcontroller pin mapping definitions
#define DHTPIN 15        // Digital pin connected to DHT22 Data
#define DHTTYPE DHT22    // Specifying the DHT sensor variant
#define MQ5_PIN 34       // Analog pin (ADC1_CH6) connected to MQ-5 output

// Instantiate sensor and display objects
DHT dht(DHTPIN, DHTTYPE);
LiquidCrystal_I2C lcd(0x27, 16, 2); // Standard I2C address 0x27 for 16x2 Display

void setup() {
  // Initialize Serial Interface for local terminal debugging
  Serial.begin(115200);
  Serial.println("--- Viltrum Regents Greenhouse System Initializing ---");

  // Initialize DHT22 Sensor
  dht.begin();
  
  // Initialize and light up the I2C LCD Screen
  lcd.init();
  lcd.backlight();
  
  // Display loading splash screen for the professor
  lcd.setCursor(0, 0);
  lcd.print("GROUP 4 VILTRUM");
  lcd.setCursor(0, 1);
  lcd.print("Greenhouse Node");
  delay(2500); 
  lcd.clear();
}

void loop() {
  // 1. Gather micro-climate data from the DHT22
  float humidity = dht.readHumidity();
  float temperature = dht.readTemperature();

  // 2. Sample data from the Air Quality/Gas Sensor
  int rawGasValue = analogRead(MQ5_PIN);
  // Convert ESP32 12-bit ADC values (0-4095) to a clean percentage for display
  float gasPercentage = (rawGasValue / 4095.0) * 100.0;

  // 3. Exception handling: Check if sensors are disconnected or miswired
  if (isnan(humidity) || isnan(temperature)) {
    Serial.println("Hardware Error: Unable to read from DHT22!");
    lcd.setCursor(0, 0);
    lcd.print("Sensor Fault:   ");
    lcd.setCursor(0, 1);
    lcd.print("Check DHT Wires ");
    delay(2000);
    return; // Force a loop restart to protect data stream integrity
  }

  // 4. Output clean execution data directly to the Serial Monitor
  Serial.print("Temp: "); Serial.print(temperature, 1); Serial.print("°C | ");
  Serial.print("Hum: "); Serial.print(humidity, 1); Serial.print("% | ");
  Serial.print("Gas: "); Serial.print(gasPercentage, 1); Serial.println("%");

  // 5. Update the 16x2 Screen 
  // Line 1 Formatting: Temp & Humidity side-by-side
  lcd.setCursor(0, 0);
  lcd.print("T:");
  lcd.print(temperature, 1);
  lcd.print("C H:");
  lcd.print(humidity, 1);
  lcd.print("% "); // Trailing space avoids leftover characters during flux

  // Line 2 Formatting: Real-time Gas Threshold tracking
  lcd.setCursor(0, 1);
  lcd.print("Gas Lvl: ");
  lcd.print(gasPercentage, 1);
  lcd.print("%   "); // Trailing spaces clears the display lines completely

  // DHT22 internal logic demands a minimum 2-second sleep step between reads
  delay(2000); 
}

#### Architecture (c) Code Script (`sketch.ino`)
```cpp
#include <DHT.h>
#include <esp_chip_info.h>
#include <esp_system.h>

// --- PIN ASSIGNMENTS ---
// Master Node Pins (ESP32 #1)
#define DHTPIN 15
#define DHTTYPE DHT22
#define RELAY_PIN 12

// Slave Node Pins (ESP32 #2)
#define MQ5_PIN 34
#define INTERFACE_SIGNAL_PIN 14

DHT dht(DHTPIN, DHTTYPE);
bool isMasterNode = false;

// Function to uniquely identify which board is executing the code
void identifyBoard() {
  uint64_t chipid = ESP.getEfuseMac(); // Get unique MAC address of the ESP32
  uint16_t chip = (uint16_t)(chipid >> 32);
  
  Serial.begin(115200);
  delay(500);
  Serial.println("\n--------------------------------------------------");
  Serial.print("Booting Node with Unique ID: ");
  Serial.println(chip);

  // In Wokwi, the first board created and the second board created will have 
  // different internal MAC IDs. We sample the ID on boot.
  // Note: For simulation flexibility, we can also use a jumper wire trick:
  // If a specific pin (e.g., GPIO 0) is wired to GND on one board, it becomes the slave.
  // Let's use a fail-safe Digital Pin check instead of MAC IDs for easy Wokwi setup!
}

void setup() {
  Serial.begin(115200);
  delay(500);
  
  // --- JUMPER WIRE ROLE SELECTION ---
  // To tell Wokwi which board is which:
  // On your MASTER ESP32, leave GPIO 4 empty.
  // On your SLAVE ESP32, connect a wire from GPIO 4 straight to GND.
  pinMode(4, INPUT_PULLUP);
  delay(10);
  
  if (digitalRead(4) == HIGH) {
    isMasterNode = true;
    Serial.println(">>> ROLE DETERMINATION: MASTER NODE ACTIVATED <<<");
    
    // Initialize Master Hardware
    pinMode(RELAY_PIN, OUTPUT);
    digitalWrite(RELAY_PIN, LOW);
    dht.begin();
  } else {
    isMasterNode = false;
    Serial.println(">>> ROLE DETERMINATION: SLAVE NODE ACTIVATED <<<");
    
    // Initialize Slave Hardware
    pinMode(INTERFACE_SIGNAL_PIN, INPUT_PULLDOWN); 
  }
}

void loop() {
  if (isMasterNode) {
    // ==========================================
    // EXECUTION LOOP FOR MASTER NODE (ESP32 #1)
    // ==========================================
    float temp = dht.readTemperature();
    
    if (isnan(temp)) {
      Serial.println("[MASTER] Error: DHT22 Disconnected!");
      delay(2000);
      return;
    }

    Serial.print("[MASTER] Greenhouse Temp: "); 
    Serial.print(temp, 1); 
    Serial.println("°C");

    // Automation: If temperature crosses critical threshold (30C), trip the relay
    if (temp > 30.0) {
      digitalWrite(RELAY_PIN, HIGH);
      Serial.println("[MASTER] Alert: Threshold Exceeded! Energizing Relay (Sending HIGH signal)...");
    } else {
      digitalWrite(RELAY_PIN, LOW);
      Serial.println("[MASTER] Climate Normal. Relay De-energized (Sending LOW signal)...");
    }
    
  } else {
    // ==========================================
    // EXECUTION LOOP FOR SLAVE NODE (ESP32 #2)
    // ==========================================
    int rawGas = analogRead(MQ5_PIN);
    float gasPct = (rawGas / 4095.0) * 100.0;
    
    // Read the incoming signal passed across the isolated relay contacts
    int relaySignalInput = digitalRead(INTERFACE_SIGNAL_PIN);

    Serial.print("[SLAVE] Local Gas Sensor: "); 
    Serial.print(gasPct, 1); 
    Serial.print("% | Inter-Board Relay Bus Status: ");
    
    if (relaySignalInput == HIGH) {
      Serial.println(" CRITICAL ALERT RECEIVED FROM MASTER!");
    } else {
      Serial.println("Clear ");
    }
  }

  delay(2000); // Synchronized tick rate for both nodes
}

### 3. Engineering Implementation Details & Assumptions
* **MQ-5 Gas Sensor Representation:** Because Wokwi does not provide a native dedicated gas sensor block in its basic menu, a 3-pin sliding potentiometer was engineered into the layout to output variable voltage ranges (0 to 3.3V). The ESP32 accurately processes this as a 12-bit ADC value (0-4095) mapped linearly to air quality metrics.
* **Architecture C Dual-Core Simulation Strategy:** To circumvent the Wokwi browser constraint of only building one active execution script per project, a single integrated firmware package was compiled. Role selection is determined at startup via a physical hardware jumper, a ground constraint on `GPIO 4` activates the Slave Node, while leaving it disconnected defaults the board to the Master Node state.

### 4. Evidence of Groupwork & Task Allocations

#### Phase 1: Simulation & Virtual Prototyping (Completed)
* **Trevor James (167612):** Authored the Master/Slave architecture separation logic and unified firmware for the dual-board simulation.
* **Wesley Mutisya (132989):** Designed the circuit schematics for both Wokwi workspaces and completed layout verification.
* **Bill Otieno (163362):** Drafted the DHT22 climate data scaling algorithms and simulation exception handlers.
* **Nicole Kirimi (147585):** Implemented the virtual I2C LCD custom formatting layers and display data buffers.
* **Jeremy Chege (148654):** Ran validation testing on the analog ADC percentage mappings for the gas sensor inputs.
* **Lorna Nyabuto (142544):** Organized the Git version repository structure and compiled the documentation.

#### Phase 2: Physical Lab Implementation & Assembly Tasks
* **Trevor James & Wesley Mutisya:** Responsible for physical board flashing and hardware circuit wiring. They will configure the physical MQ-5 sensor's VCC line to the stable 5V (VIN) pin, wire the logic signal line to GPIO 34, and connect the physical relay contacts safely to isolate the Master and Slave voltage paths.
* **Bill Otieno & Jeremy Chege:** Responsible for real-world signal testing and sensor debugging. They will use a multimeter to check voltage lines, verify that the physical DHT22 pulls up cleanly without throwing hardware faults, and track real-time changes using the Arduino IDE Serial Monitor.
* **Nicole Kirimi & Lorna Nyabuto:** Responsible for physical display calibration and lab report logging. They will adjust the physical hardware potentiometer on the back of the I2C LCD board to calibrate character contrast, verify that live readings refresh correctly on the screen every 2 seconds, and document the final system runtime observations.
