# ICS 4111 — Group 4 Project Meeting Minutes

**Course:** ICS 4111 — Embedded Systems & IoT
**Semester:** April – July 2026
**Project:** Flora Farms Greenhouse Monitoring System — Daisy (Gerbera)
**Group:** Viltrum Regents (Group 4)
**Instructor:** Mr. A. Vikiru

## Group Members

| Name | Role |
|---|---|
| Wesley Mutisya | Member — Question 1 (Growth Requirements) |
| Jeremy Chege | Member — Question 2 (Hardware Components) |
| Nicole Kirimi | Secretary — Question 3 (Datasheets) |
| Bill Ritchie | Member — Question 4, Design A (Hub) |
| Trevor James | Member — Question 4, Design B (Two ESP32s) |
| Lorna Nyabuto | Member — Question 4, Design C (Chain with Relay) |

---

## Meeting 1 — Project Planning and Task Allocation

**Date:** Thursday, 28 May 2026
**Time:** 2:00 pm – 3:15 pm
**Venue:** Strathmore University, Gazebos behind SBS
**Chairperson:** Lorna Nyabuto
**Secretary:** Nicole Kirimi
**Present:** Wesley Mutisya, Jeremy Chege, Nicole Kirimi, Bill Ritchie, Trevor James, Lorna Nyabuto
**Apologies:** None

### Agenda

1. Review of Deliverable 1 requirements
2. Confirmation of assigned flower species
3. Task allocation among members
4. Timeline and milestones
5. Logistics and any other business (AOB)

### 1. Review of Deliverable 1 requirements

The group walked through the *Semester Project Overview* and *Deliverable 1* briefs collectively. Lorna summarised the four questions: (Q1) environmental growth requirements for the assigned flower, (Q2) full hardware components list, (Q3) datasheets for five specified components, and (Q4) three schematic architectures. The mandatory groupwork-evidence requirement and the associated 50 % penalty for non-compliance were emphasised. It was agreed that the deliverable would be submitted as Markdown (`.md`) files in a shared GitHub repository.

### 2. Confirmation of assigned flower species

The group was assigned **"daisy"** per the project-allocation document. After discussion, the members agreed that the write-up would be based on the **Gerbera daisy (*Gerbera jamesonii*)** since it is the dominant commercial cut-flower daisy in Naivasha and a strong fit for the Flora Farms export scenario described in the brief. The species choice would be briefly justified in the introduction of the deliverable. 

### 3. Task allocation

Members volunteered for the following responsibilities, accepted unanimously:

| Member | Allocated Task |
|---|---|
| Wesley Mutisya | Question 1 — growth-requirement research, descriptive prose, and summary table for Gerbera daisy |
| Jeremy Chege | Question 2 — hardware components list covering all Q1 parameters plus LPG sensing; grouped by functional role |
| Nicole Kirimi | Question 3 — sourcing and verification of datasheets for the five specified components (ESP32-S, DHT22, MQ-5, OLED, relay) |
| Bill Ritchie | Question 4 Design A — single ESP32-S hub with MQ-5, DHT22, and OLED |
| Trevor James | Question 4 Design B — two ESP32-S boards directly interfaced via UART |
| Lorna Nyabuto | Question 4 Design C — chain architecture with relay-gated power between two ESP32-S nodes |

Lorna additionally accepted responsibility for managing the GitHub repository, and it was agreed that each member would send their work on that same repository.

### 4. Timeline and milestones

| Milestone | Target Date |
|---|---|
| Individual sections drafted | Thursday, 28 May 2026 |
| Group cross-review and merge session | Friday 5 June 2026 |
| Final compilation and GitHub commit | Monday 8 June 2026 |

### 5. Logistics and AOB

- Ritchie and Trevor agreed to coordinate on a consistent schematic style across Designs A, B, and C using EasyEDA.
- All members agreed to adopt **Zotero** for reference management to standardise citations across sections where needed.
- Lorna to set up the shared GitHub repository and share the link with all members by the next week.
- Discussion noted that the Makerspace lab MAY be needed in a later deliverable for physical prototyping; no booking required at this stage.

### Resolutions / Action Items

| # | Action | Owner | Deadline |
|---|---|---|---|
| 1 | Draft individual section | All members (per allocation) | 28 May 2026 |
| 2 | Set up GitHub repository | Lorna Nyabuto | 28 May 2026 |
| 3 | Standardise schematic style across all three designs | Bill Ritchie, Trevor James | By 30 May 2026 |

**Meeting adjourned:** 3:15 pm
**Next meeting:** Friday, 5 June 2026

---

## Meeting 2 — Progress Review and Compilation

**Date:** Friday, 5 June 2026
**Time:** 12:00 pm - 1:00 pm
**Venue:** Strathmore University, Gazebos behind SBS
**Chairperson:** Lorna Nyabuto
**Secretary:** Nicole Kirimi
**Present:** Wesley Mutisya, Jeremy Chege, Nicole Kirimi, Bill Ritchie, Trevor James, Lorna Nyabuto
**Apologies:** None

### Agenda

1. Section-by-section review of drafted work
2. Identification of gaps and inconsistencies
3. Schematic styling and consistency
4. Group photograph for evidence
5. Final compilation tasks
6. AOB

### 1. Section-by-section review

Each member presented the draft of their assigned section to the group:

- **Wesley (Q1)** presented the Gerbera growth-requirements table covering temperature, humidity, soil type, soil moisture, soil pH, and sunlight. The group discussed whether the volumetric water content range (25–35 % VWC) was sufficiently supported by sources. It was agreed to retain the figure alongside the qualitative description (~25 mm of water per week) and cite both industry and academic sources.
- **Jeremy (Q2)** presented the hardware components list. Discussion centred on whether to include the soil moisture sensor, pH sensor, and light sensor — components needed for Question 1's parameters but absent from Question 3's named-five list. The group agreed to include them with a note explaining the scope distinction between Q2 (comprehensive system) and Q4 (schematics restricted to the five specified components).
- **Nicole (Q3)** confirmed that all five datasheets had been sourced and verified — ESP32-WROOM-32 (Espressif), DHT22/AM2302 (Aosong), MQ-5 (Hanwei / Winsen), SH1106 OLED (Univision), and SRD-05VDC-SL-C relay (Songle). Both chip-level and module-level references were included where applicable.
- **Bill (Design A)**, **Trevor (Design B)**, and **Lorna (Design C)** presented their EasyEDA schematic drafts. Trevor's UART link in Design B was discussed, and the group agreed that crossed TX/RX with a shared common ground was the correct interpretation of "directly interfaced". Lorna's Design C generated the longest discussion because of its dual-rail power architecture (always-on `+5V` and switched `+5V_SW`); the group verified that the relay's COM-NO contacts gate the second ESP32's power supply correctly.

### 2. Gaps identified

- Group-work evidence section needed to be added to the deliverable. Nicole agreed to compile the two sets of meeting minutes.
- Each schematic needed labelled GPIO pin numbers matching the build specification.
- References list needed an APA 7th-edition pass before submission.

### 3. Schematic styling

The group agreed all three schematics would be exported as **PNG files at 300 DPI** from EasyEDA and placed in a `/schematics/` folder in the repository. Each design's source `.json` file would also be committed so the marker could open the originals if required.

### 4. Group photograph

The group did not take a group photograph. Instead, these minutes were written as evidence.

### 5. Final compilation tasks

| Task | Owner | Deadline |
|---|---|---|
| Commit EasyEDA exports (PNG + JSON) to `/schematics/` | Bill, Trevor, Lorna | Sunday 7 June 2026 |
| Final group review of final documents | All members | Before deadline |
| Submit GitHub link on e-learning | Lorna Nyabuto | Per submission deadline |

### 6. AOB

The group held a brief discussion on the upcoming firmware-development phase of the semester project and noted that responsibilities for that phase would be reallocated in a future meeting.

**Meeting adjourned:** 1:15 pm

---

## Authentication

These minutes were recorded by **Nicole Kirimi** in her capacity as group secretary and reviewed by all members present.

| Signed | Name | Role |
|---|---|---|
| _______________ | Nicole Kirimi | Secretary |
| _______________ | Lorna Nyabuto | Chairperson (Meeting 1) |
| _______________ | Lorna Nyabuto | Chairperson (Meeting 2) |
