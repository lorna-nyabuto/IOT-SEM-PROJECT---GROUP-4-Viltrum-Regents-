# ICS 4111: Embedded Systems & IoT — Viltrum Regents Semester Project Deliverable 3
## Group Work Session Minutes

**Dates:** Thursday, 9th July 2026 | Friday, 10th July 2026
**Time:** 9th July: 9:00 am – 12:00 pm | 10th July: 9:30 am – 11:00 am
**Venue:** Engineering Lab
**Prepared by:** Nicole Kirimi

### Attendees
1. Lorna Nyabuto - 142544
2. Wesley Mutisya - 132989
3. Jeremy Chege - 148654
4. Bill Otieno - 163362
5. Trevor James - 167612
6. Nicole Kirimi - 147585

### Apologies
None.

### Purpose of Session

To develop the prototype required for Deliverable 3: transmitting and visualizing greenhouse sensor data (temperature, humidity, gas levels) on cloud platforms (InfluxDB Cloud and Grafana), using the ESP32-S + MQ-5 + DHT22 + LCD architecture carried over from Deliverables 1 and 2.

### Task Allocation and Progress

| Task | Assigned To | Status |
|---|---|---|
| Physical breadboard build and firmware flashing attempt (ESP32-S + MQ-5 + DHT22 + LCD) | Lorna Nyabuto, Bill Otieno, Wesley Mutisya | Attempted — blocked |
| Troubleshooting Arduino IDE / ESP32-S board recognition issue | Jeremy Chege, Nicole Kirimi, Trevor James | Attempted — unresolved |
| Wokwi simulation build (wiring + firmware) | Nicole Kirimi, Lorna Nyabuto | Completed |
| InfluxDB Cloud bucket setup and line-protocol write integration | Wesley Mutisya, Bill Otieno | Completed |
| Grafana dashboard configuration (data source + 3 panels) | Trevor James, Jeremy Chege | Completed |
| Deliverable documentation and repository compilation | Nicole Kirimi/Lorna Nyabuto | Completed |

### Summary of Work Done

- The group met in the lab to assemble and test the physical prototype using the ESP32-S, DHT22, MQ-5, and LCD as specified in the deliverable.
- Lorna, Bill, and Wesley worked on assembling and testing the physical prototype in the lab.
- During testing, the Arduino IDE failed to correctly recognize/select the ESP32-S board, preventing firmware upload to the physical device. Jeremy Chege, Nicole Kirimi, and Trevor James led the troubleshooting of board manager settings, port selections, and drivers, but could not resolve the issue within the session time available.
- Given the time constraint, the group collectively decided to proceed with a Wokwi simulation instead, as explicitly permitted by the deliverable instructions.
- Nicole and Lorna built the Wokwi simulation, replicating the same wiring architecture (ESP32-S + DHT22 + gas sensor + I2C LCD).
- Wesley and Bill set up the InfluxDB Cloud bucket and implemented the line-protocol write integration from the ESP32 firmware.
- Trevor and Jeremy configured the Grafana dashboard, connecting it to InfluxDB and building the three visualisation panels (temperature, humidity, gas level).
- Nicole Kirimi and Lorna Nyabuto compiled the deliverable documentation and repository.
- Although the simulation and cloud setup were configured under one member's account/laptop for practical convenience, all members contributed to decisions on wiring, code logic, and dashboard design throughout the session.

### Issues Encountered

- The Arduino IDE did not correctly reflect/recognize the ESP32-S board, which was the primary blocker preventing the physical implementation from being completed.
- Time constraints within the lab session meant the group could not fully resolve the IDE/board issue before the session ended, prompting the switch to simulation on Wokwi.

### Action Items / Next Steps

| Action | Owner | Due |
|---|---|---|
| Capture images of the physical lab attempt | All group members | Before submission |
| Publish Wokwi project as public and extract shareable link | Trevor James, Bill Otieno | Before submission |
| Confirm InfluxDB and Grafana public links/screenshots | Jeremy Chege, Wesley Mutisya | Before submission |
| Compile final Markdown deliverable document in GitHub repo | Nicole Kirimi/Lorna Nyabuto | Before due date |
| Submit repo link to e-learning | Nicole Kirimi/Lorna Nyabuto | Due date |

---

*Minutes compiled for inclusion in the Deliverable 3 submission repository.*
