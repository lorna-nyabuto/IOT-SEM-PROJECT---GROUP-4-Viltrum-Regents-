# ICS 4111: Embedded Systems & IoT — Semester Project Deliverable 2
## Group Work Session Minutes

**Dates:** 24th June 2026 and 29th June 2026
**Time:** 24th June — 3:00 PM to 5:00 PM | 29th June — 9:00 AM to 12:00 Noon
**Venue:** Engineering Lab
**Prepared by:** Lorna Nyabuto

### Attendees
- Lorna Nyabuto
- Nicole Kirimi
- Jeremy Chege
- Bill Ritchie
- Trevor James

### Apologies
None.

### Purpose of Session
To develop the physical and simulated prototypes required for Deliverable 2, covering:
- **Architecture (a):** ESP32 + MQ-5 + DHT22 + I²C LCD (physical + simulated)
- **Architecture (b):** ESP32-A (MQ-5) interfaced with ESP32-B (DHT22) via UART (physical)
- **Architecture (c):** ESP32-A (DHT22 + relay) interfaced with ESP32-B (MQ-5) (simulated)

### Task Allocation and Progress

| Task | Assigned To | Status |
|---|---|---|
| Physical breadboard build — Architecture (a): ESP32 + MQ-5 + DHT22 + LCD | Lorna Nyabuto, Nicole Kirimi, Jeremy Chege, Bill Ritchie | Completed |
| Physical build — Architecture (b): two-node UART (ESP32-A + ESP32-B) | Lorna Nyabuto, Nicole Kirimi, Jeremy Chege, Bill Ritchie | Completed |
| Wokwi simulation — Architecture (a) | Trevor James | Completed |
| Wokwi simulation — Architecture (c): relay-based | Trevor James | Completed |

### Summary of Work Done
- Lorna, Nicole, Jeremy, and Bill worked jointly in the lab on the physical builds for architectures (a) and (b), including component wiring, resistor placement for the MQ-5 and DHT22 sensors, I²C LCD integration, and UART communication setup between the two ESP32 nodes.
- Trevor James independently developed the Wokwi simulations for architectures (a) and (c), including circuit layout, code implementation, and verification of sensor/relay output on the simulated LCD and serial monitor.
- The group cross-checked that architecture (b) was done physically and architecture (c) was done in simulation, satisfying the interchangeability requirement in the deliverable instructions.

### Issues Encountered
- Several components (MQ-5 gas sensor, DHT22, I²C LCD) were new to the group, resulting in a learning curve around correct wiring, resistor placement, and library usage.
- The Arduino IDE was occasionally temperamental, particularly around board/port detection and IntelliSense configuration during the UART setup. These issues were worked through and resolved by the team.

### Action Items / Next Steps

| Action | Owner | Due |
|---|---|---|
| Capture images of working physical prototypes and IDE/LCD output | Lorna Nyabuto, Nicole Kirimi, Jeremy Chege, Bill Ritchie | Before submission |
| Publish Wokwi projects as public and extract shareable links | Trevor James | Before submission |
| Compile final Markdown deliverable document in GitHub repo | Lorna Nyabuto | Before due date |
| Submit repo link to e-learning | Lorna Nyabuto | Due date |

---
*Minutes compiled for inclusion in the Deliverable 2 submission repository.*
