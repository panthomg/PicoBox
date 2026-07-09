<img width="16219" height="7525" alt="Untitled Document 2 (2)" src="https://github.com/user-attachments/assets/4dca9b9f-4092-44d4-b167-6453fcab0359" />

# Everything about the hardware of Pico
<img width="6969" height="1611" alt="Untitled Document 2 (1) (1) (3)" src="https://github.com/user-attachments/assets/bbe95f63-0310-4345-9dbe-734af74f7c62" />

Here is the cleaned and properly formatted markdown documentation for your project, with all price data removed and a polished structure for high scannability.

---

## Core Components

<img width="6969" height="2346" alt="Untitled Document 2 (1) (1) (2)" src="https://github.com/user-attachments/assets/3659fd40-ad36-4d4c-a595-1e3cc0a8aafe" />



### The Brain: Arduino UNO Q 4GB

> **Overview:** The central processing unit handling the system's logic, AI processing, and OS environment.

| Specification | Detail |
| --- | --- |
| **Processor** | Qualcomm QRB2210 (quad-core 2.0GHz) |
| **RAM** | 4GB LPDDR4 |
| **Storage** | 32GB eMMC |
| **GPU** | Adreno 702 |
| **AI Accelerator** | Qualcomm AI Engine |
| **Connectivity** | Wi-Fi 5 (802.11ac), Bluetooth 5.1 |
| **OS** | Debian Linux (dual-processor architecture) |

### The Ears: ReSpeaker XVF3800 4-Mic Array

> **Overview:** Responsible for far-field voice capture, audio processing, and spatial voice tracking.

| Specification | Detail |
| --- | --- |
| **Microphones** | 4 MEMS digital microphones |
| **Processor** | XMOS XVF3800 |
| **Range** | Up to 5 meters (far-field) |
| **Coverage** | 360° voice tracking |
| **Features** | Beamforming, Noise Suppression, Acoustic Echo Cancellation (AEC), Direction of Arrival (DoA) |
| **Interface** | USB / I2S |

### The Mouth: Speaker

> **Overview:** The primary audio output component for voice responses and feedback.

| Specification | Detail |
| --- | --- |
| **Type** | USB-powered 2.0 Speaker |
| **Output** | 2 x 3W drivers |
| **Connectivity** | USB + 3.5mm AUX |
| **Alternative** | JBL GO 3 (Bluetooth) for prototyping |

---

## 4.2 Complete Bill of Materials (BOM)

| Component | Model |
| --- | --- |
| **Main Board** | Arduino UNO Q 4GB |
| **Mic Array** | ReSpeaker XVF3800 Flex 4-Mic |
| **Speaker** | USB 2.0 Speaker |
| **Power Supply** | 5V/3A USB-C Adapter |
| **USB Hub** | 4-in-1 USB-C Hub |

---

## 4.3 Alternative Budget Build

| Component | Model |
| --- | --- |
| **Main Board** | Arduino UNO Q 2GB |
| **Mic Array** | ReSpeaker Lite 2-Mic |
| **Speaker** | USB 2.0 Speaker |
| **Power Supply** | 5V/3A USB-C Adapter |

---

## 4.4 Physical Design Specifications

| Aspect | Specification |
| --- | --- |
| **Form Factor** | Cube (Steam Machine style) |
| **Dimensions** | ~152mm (6 inches) per side |
| **Material** | 3D-printed PLA (prototype), PETG/ABS (final) |
| **Weight** | ~500g (estimated) |
| **Ports** | USB-C (power), USB-A (accessories), 3.5mm AUX |
