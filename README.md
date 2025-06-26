# NVNT's SDEX2M2 (MicroSD Express to M.2) Adapter Project

![image](https://github.com/user-attachments/assets/679e10da-82e8-4d7a-8257-d86a05efd59d)

SDEX2M2 (Micro**SD** **Ex**press to **M2**) is an adapter for the Nintendo Switch 2 which converts the MicroSD Express slot to a NVME M.2 (M-Key) slot. Think MicroSD Express cards are difficult to find or expensive? Looking to expand your storage for cheaper? Just use the NVME M.2 SSD that you have, and/or can easily find! The project is open source hardware under the GPLv3 License.

This project also encompasses the sister-project of "MicroSD Express to SD Express" adapter, which is a pin-to-pin conversion kit allowing full size SD Express cards to be used on the Nintendo Switch 2.

---

## 📚 Table of Contents
- **Introduction**
  - [Goals](#goals)
  - [Status](#status)
  - [Warnings](#warnings)
- **Assets & Hardware Info**
  - [Bill of Materials (BOM)](#bill-of-materials-bom)
  - [PINOUT & LEGEND](#pinout--legend)
    - [MicroSD Express to M.2 NVMe Mapping](#microsd-express-to-m2-nvme-mapping)
    - [M.2 NVMe Pinout](#m2-nvme-pinout)
    - [MicroSD Express Pinout](#microsd-express-pinout)
- **PCB's / Boards**
  - [Wiring Schematic](#wiring-schematic)
  - [MicroSD Express Dummy Card](#microsd-express-dummy-card)
  - [MicroSD Express Breakout Board](#microsd-express-breakout-board)
  - [NVMe M.2 SSD Breakout Board](#nvme-m2-ssd-breakout-board)
  - [MicroSD Express to SD Express Prototype Adapter](#microsd-express-to-sd-express-prototype-adapter)
  - [SDEX2SDEX MicroSD Express to NVMe M.2 Prototype Pin-to-Pin Adapter](#sdex2sdex-microsd-express-to-nvme-m2-prototype-pin-to-pin-adapter)


---

## How is this possible?

This is possible because the Nintendo Switch 2's MicroSD Express slot supports the SD Express 7.1 standard, which exposes a **true PCIe Gen3 x1 interface** and utilizes the **NVMe protocol** for communication.

This adapter simply maps PCIe x1 from the Switch 2’s MicroSD Express slot to a standard M.2 2230 NVMe SSD. After further research and review from users, an onboard mcu/fpga will be required for the handshake provess with the Switch 2.

---

## Goals

- ✅ Create Pinout & Pin Definitions (UPDATED!)
- ✅ Create Footprints for MicroSD Express
- ✅ Create Schematic for PCB layout
- ✅ Create Dummy MicroSD Express Card V2
- ✅ Create M.2 Breakout for prototyping (Updated 2-layer PCB)
- ✅ Create MicroSD Express Breakout Board V0.1 (Updated 2-layer PCB)
- ✅ Create MicroSD Express to SD Express Adapter (Experimental, Updated 2-layer PCB)
- ✅ Create BOM for fabrication and sourcing (WIP)
- ✅ Create MicroSD Express to NVMe M.2 SSD Pin to Pin Adapter (Proof of concept)
- 🔲 Create MicroSD Express to NVMe M.2 SSD Adapter with FPGA/MCU Proto (for handshake with Nintendo Switch 2)
- 🔲 Create MicroSD Express to NVMe M.2 SSD Dock/Flex Cable Setup

---

## Status

Work in progress. 

Currently, an early proof of concept prototype of the SDEX2M2 MicroSD Express to NVMe M.2 SSD Adapter has been made. 

Additionally, production-ready (hopefully!) 2-layer PCBs for the MicroSD Express breakout board, and the NVMe breakout board have been uploaded.

The MicroSD Express to SD Express (full size) adapter production ready board has been uploaded too.

---

## Warnings

- Use at your own risk. We are **not liable** for any damage to your drive, Switch 2, or other devices.
- Only use **low-voltage, low-power M.2 2230 NVMe drives**.
- **Do not use this in legacy MicroSD slots** (e.g., original Nintendo Switch).
  
---

## Bill of Materials (BOM)

| Reference | Quantity | Description                             | Part Number        | Manufacturer   |
|-----------|----------|-----------------------------------------|--------------------|----------------|
| J2        | 1        | M.2 Socket (M-Key, 2230)                | 114020             | Amphenol       |
| FB1       | 1        | Ferrite Bead 220Ω@100MHz 0603           | BLM18PG221SN1D     | Murata/OEM     |
| PCB       | 1        | 4-Layer PCB        | N/A                | Fabricated         | *              |
|*          | 1        | 10kΩ – 100kΩ Pull Up Resistor (Optional) | N/A               | *              |

The optional resistor is for the PERST# lane, may help with state when idle. Not sure if needed until prototyping commences.

---

## PINOUT & LEGEND

### MicroSD Express to M.2 NVMe Mapping

| microSD Express Pin  | PCIe Function | M.2 M-Key Pin(s) | M.2 Function         |
| -------------------- | ------------- | ---------------- | -------------------- |
| 7 (Row 1)            | REFCLK+       | B10              | REFCLK+              |
| 8 (Row 1)            | REFCLK−       | B11              | REFCLK−              |
| 2 (Row 1)            | PERST#        | A11              | PERST#               |
| 1 (Row 1)            | CLKREQ#       | B8               | CLKREQ#              |
| 11 (Row 2)           | TX+           | B23              | PCIe TX+             |
| 12 (Row 2)           | TX−           | B24              | PCIe TX−             |
| 14 (Row 2)           | RX-           | A21              | PCIe RX+             |
| 15 (Row 2)           | RX+           | A22              | PCIe RX−             |
| 4 (Row 1)            | 3.3V VDD      | B2, B3, B4       | 3.3V Power           |
| 6, 10, 13, 16     | GND           | A1, A4, etc.     | Ground               |

---

### M.2 NVMe Pinout

| Pin     | Name     | Function                 |
|---------|----------|--------------------------|
| A11     | PERST#   | PCIe Reset               |
| A21     | RX+      | PCIe RX+ (to host)       |
| A22     | RX−      | PCIe RX− (to host)       |
| B10     | REFCLK+  | PCIe Reference Clock +   |
| B11     | REFCLK−  | PCIe Reference Clock −   |
| B23     | TX+      | PCIe TX+ (from host)     |
| B24     | TX−      | PCIe TX− (from host)     |
| B2–B4   | 3.3V     | Power Supply             |
| A1, A4  | GND      | Ground Pins              |

---

### MicroSD Express Pinout

In SD Mode &* PCIe Mode

| Pin | Row 1 Contact | SD Mode Function | PCIe Mode Function               |
| --- | ------------- | -------------------- | ---------------------------- |
| 1   | DAT2          | Data Line 2          | CLKREQ# (Power / Signal Mgmt)         |
| 2   | DAT3 / CD     | Data Line 3 / CD     | PERST# (Reset)               |
| 3   | CMD           | Command Line         | CMD (unused in PCIe mode)    |
| 4   | VDD           | 3.3V Power           | 3.3V Power                   |
| 5   | CLK           | Clock Line           | CLK (unused in PCIe mode)    |
| 6   | VSS           | Ground               | Ground                       |
| 7   | DAT0          | Data Line 0          | REFCLK+ (PCIe Ref Clock)     |
| 8   | DAT1          | Data Line 1          | REFCLK− (PCIe Ref Clock)     |


| Pin | Row 2 Contact   | PCIe Function                 |
| --- | --------------- | ----------------------------- |
| 9   | 1V8             | 1.8 Volts                     |
| 10  | VSS2            | Ground for isolation          |
| 11  | TX+             | PCIe TX+ (Transmit)           |
| 12  | TX-             | PCIe TX- (Transmit)           |
| 13  | VSS3            | Ground for isolation          |
| 14  | RX-             | PCIe RX- (Receive)            |
| 15  | RX+             | PCIe RX+ (Receive)            |
| 16  | VSS4            | Ground for isolation          |
| 17  | 1V2             | 1.2 Volts                     |

Please note: Row 2 is only operational in PCIe Mode. Row 2 is based on M1cha's (https://github.com/M1cha/sdexpress_pcbs) schematic.

---

### MicroSD Express Card to SD Express Slot Pinout

| **MicroSD Express Pin** | **Function (PCIe Mode)**  | **SD Express Slot Pin** | **Function in Slot** | 
| ----------------------- | ------------------------- | ----------------------- | -------------------- | 
| 1 DAT2                  | CLKREQ#                   | 51                      | CLKREQ# (Power / Signal Mgmt) | 
| 2 DAT3 / CD             | PERST#                    | 52                      | PERST# (Reset line)  |
| 3 CMD                   | CMD (unused)              | —                       | CMD (unused in PCIe mode) | 
| 4 VDD                   | 3.3V VDD                  | 18, 48                  | VDD                  |
| 5 CLK                   | CLK (unused)              | —                       | —                    | 
| 6 VSS                   | GND (VSS1)                | 17, 47, 49, 50          | GND                  |
| 7 DAT0                  | REFCLK+                   | 45                      | REFCLK+              | 
| 8 DAT1                  | REFCLK−                   | 46                      | REFCLK−              | 
| 9 1V8                   | 1.8V VDD (VDD2)           | 1, 2, 3 (often shared)  | VDD 1.8 Volts        | 
| 10 VSS2                 | GND (VSS2)                | 17, 47, etc.            | GND (GND Ground for isolation)| 
| 11 TX+                  | TX+                       | 39                      | PCIe TX+ (Transmit)  |
| 12 TX-                  | TX−                       | 41                      | PCIe TX- (Transmit)  |
| 13 VSS3                 | GND  (VSS3)               | 17, 47, etc.            | GND (Ground for isolation)| 
| 14 RX-                  | RX−                       | 35                      | PCIe RX- (Receive)|
| 15 RX+                  | RX+                       | 37                      | PCIe RX+ (Receive)|
| 16 VSS4                 | GND (VSS4)                | 17, 47, etc.            | GND (Ground for isolation)|                 
| 17 1V2                  | 1.2V VDD (VDD3, optional) | —                       | Not used (May be unused)|

Note: WIP

---

### Wiring Schematic

![image](https://github.com/user-attachments/assets/4307b001-33de-480f-b8d2-8748455a149e)

Still a WIP. Some discrepencies may exist.

---

### MicroSD Express Dummy Card

A dummy card has been created (thanks to M1cha's design examples!), for reference. Files have been attached.

![image](https://github.com/user-attachments/assets/9f630c3f-1d3a-49ea-a7c7-d65ca15c190f)

---

### MicroSD Express Breakout Board

A production-ready 2-layer breakout board for MicroSD Express has been created (codenamed: "The Key"). Files have been attached in the repo. The purpose of this is for prototyping with a breadboard.

![image](https://github.com/user-attachments/assets/4a90a0a4-8f00-47b9-b7c8-c64651572659)


---

### NVMe M2 SSD Breakout Board

A breakout board for a NVMe M.2 SSD slot (M-key) has been created. Files have been attached in the repo. The purpose of this is for prototyping with a breadboard.

![image](https://github.com/user-attachments/assets/fd900180-43a0-4ebc-8bef-532b3a13d7fb)

---

### MicroSD Express to SD Express Prototype Adapter

An extremely experimental production ready MicroSD Express to **Full Size** SD Express Slot adapter has been made. The purpose of this is to allow full size SD Express cards to be inserted into the Nintendo Switch 2.

Please be aware that it is untested as of the time of writing.

![image](https://github.com/user-attachments/assets/9b83f480-f018-4ea3-ac5c-bcd25908664c)


---

### SDEX2SDEX MicroSD Express to NVMe M.2 Prototype Pin-to-Pin Adapter

A production-ready (but experimental) 2-layer PCB for the SDEX2M2 MicroSD Express to NVMe M.2 adapter has been uploaded. 

Please note that this is a pin-to-pin adapter, and is not capable of completing the handshake with Nintendo Switch 2. It is for proof of concept, and is untested as of the time of writing.

![image](https://github.com/user-attachments/assets/aca24f83-d0b5-4648-ab6a-90056126c72f)

---
