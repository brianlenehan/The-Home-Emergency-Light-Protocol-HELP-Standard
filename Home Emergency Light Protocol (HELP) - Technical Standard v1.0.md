Date: 2025-09-21  
**Title: Home Emergency Light Protocol (HELP) - Technical Standard v1.0



### **1\. Scope**

This document specifies the normative optical characteristics, temporal patterns, and minimum performance requirements for the HELP standard. It is the definitive technical reference for any hardware or software implementation seeking to be "HELP Compliant."

### **2\. Normative References**

* **ISO/CIE 11664-1:2019:** *Colorimetry — Part 1: CIE S 014-1/E:2006, Colorimetric Observers*.  
* **IEC 61966-2-1:1999:** *Multimedia systems and equipment \- Colour measurement and management \- Part 2-1: Colour management \- Default RGB colour space \- sRGB*.

### **3\. Terms and Definitions**

* **Chromaticity:** The quality of a color defined by its coordinates in a specified color space, independent of luminance.  
* **Luminance:** The intensity of light emitted from a surface per unit area in a given direction, expressed as a percentage of the device's maximum rated output.  
* **Temporal Pattern:** The defined sequence of changes in luminance and/or chromaticity over time.  
* **Waveform:** The shape of a repeating signal as a function of time (e.g., square, sinusoidal).

### **4\. Standard Alert Specifications**

All compliant devices must be capable of generating the four patterns defined below. Tolerances are ±5% for temporal values and within a MacAdam ellipse of 3 steps for chromaticity unless otherwise specified.

| Parameter | 🔥 ALERT-FIRE | 🚨 ALERT-INTRUSION | ⚕️ ALERT-MEDICAL | ⚠️ ALERT-HAZARD |
| :---- | :---- | :---- | :---- | :---- |
| **Primary Chromaticity (CIE xy)** | **(0.68, 0.31)** (HELP Primary Red) | **(0.31, 0.32)** (HELP White, D65) | **(0.22, 0.32)** (HELP Cyan) | **(0.44, 0.50)** (HELP Yellow) |
| **Secondary Chromaticity (CIE xy)** | **(0.58, 0.41)** (HELP Secondary Orange) | N/A | N/A | N/A |
| **Pattern Name** | Flicker-Pulse | Square Wave Strobe | Dual-Peak Sinusoidal Pulse | Sinusoidal Respiration |
| **Frequency** | 3.0 Hz (avg) | **2.0 Hz** | **0.83 Hz** (50 beats per minute) | **0.2 Hz** (1 cycle per 5 seconds) |
| **Waveform** | Quasi-random | Square | Custom Sinusoid (fast attack, slow decay) | Sinusoidal |
| **Duty Cycle / Modulation** | 80% Primary, 20% Secondary | 50% ON / 50% OFF | Modulates between Min/Max Luminance | Modulates between Min/Max Luminance |
| **Luminance (Max %)** | 100% | 100% | 100% | 90% |
| **Luminance (Min %)** | 40% | 0% | 30% | 20% |
| **Verbal Description** | A rapid, chaotic pulse between Red and Orange to simulate a flame. Frequency may vary between 2.5-3.5 Hz to enhance the chaotic effect. | A precise, high-contrast strobe. 250ms full on, 250ms full off. | A "heartbeat" pattern with two quick pulses followed by a longer pause, repeating every 1.2 seconds. (PULSE-pulse...pause...) | A very slow, smooth "breathing" effect, fading from dim to bright and back over 5 seconds. |

### **5\. Conformance and Testing**

* **Device Conformance:** A lighting device is deemed conformant if it can generate the four specified alerts natively in firmware and meets all chromatic, temporal, and luminance requirements.  
* **Testing Methodology:**  
  * Chromaticity and luminance shall be verified using a calibrated spectroradiometer.  
  * Temporal patterns, including frequency and waveform, shall be verified using a high-speed photodiode and oscilloscope.  
* **Platform Conformance:** A software platform is deemed conformant if it correctly implements the API, UX, and security requirements outlined in the *HELP v1.0 Implementation Guide*.

## **Revision History | Version | Date | Author(s) | Notes | | :--- | :--- | :--- | :--- | | 1.0 DRAFT | 2025-09-21 | S.H.S. Consortium | Initial draft for review. |**
