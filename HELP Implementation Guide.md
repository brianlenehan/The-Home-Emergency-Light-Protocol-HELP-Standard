Title: HELP Protocol v1.0 \- Platform & Device Implementation Guide  
Version: 1.0 (Draft)  
Audience: Product Management, UX/UI Design, and Software Engineering Teams

### **1.0 Guiding Principles**

Implementation of the HELP protocol must adhere to the following principles:

* **Reliability:** The system must be fail-safe. Once triggered, an alert must persist even with intermittent network connectivity. Native, on-device pattern generation is mandatory.  
* **Clarity:** The user interface for configuring and managing HELP must be simple, unambiguous, and distinct from general lighting controls.  
* **Security:** Trigger mechanisms must be secure to prevent malicious activation. Only certified device classes should be permitted to activate critical alerts.  
* **User Control:** The user must have a clear and immediate method to test the system and to cancel an active alert.

### **2.0 Platform-Level Integration (HomeKit, Google Home, Alexa)**

#### **2.1 User Experience (UX) Flow**

1. **Onboarding & Education:**  
   * Introduce HELP in a dedicated "Home Safety" section of the application.  
   * Clearly explain what each light signal means using text and animated icons.  
   * Prompt the user to designate primary and secondary HELP-enabled lights (e.g., "Front Porch Light," "Garage Lights"). The UI should prioritize lights identified as 'Exterior'.  
2. **Configuration & Trigger-Linking:**  
   * The platform must automatically detect HELP-certified trigger devices (e.g., smoke alarms, security systems).  
   * Provide a simple, toggle-based interface to link a trigger to a HELP alert.  
   * *Example:* \[Smoke Detector: Living Room\] \-\> Activates \[HELP Fire Alert\] on \[Front Porch Light\].  
   * The "Medical Emergency" alert should be linked to a user-activated trigger, such as a dedicated in-app "Panic Button" or a voice command ("Hey Siri, trigger a medical HELP alert").  
3. **System Testing:**  
   * A "Test System" feature must be present.  
   * When activated, the selected light will perform the chosen pattern for 15 seconds.  
   * The app must display a confirmation dialog during the test: "Testing HELP Fire Alert. Your light is now flashing Red & Orange. This is not a real emergency."  
4. **Alert State & Deactivation:**  
   * When a HELP alert is active, the platform app must display a persistent, high-priority banner on its home screen.  
   * This banner must clearly state the active alert type and provide a large, unambiguous "CANCEL ALERT" button.  
   * Cancellation requires a secondary confirmation step to prevent accidental deactivation.

#### **2.2 API & Logic Requirements**

* Platforms must expose a dedicated HELP\_API endpoint for certified devices.  
* The API call should be singular and declarative: device.setHelpState({alert: 'FIRE', duration: 'INDEFINITE'}). The device's firmware is then responsible for generating the pattern.  
* The platform must maintain a state machine to track active alerts and ensure cancellation commands are properly relayed.

### **3.0 Device-Level Integration (Lighting & Trigger Hardware)**

#### **3.1 Firmware Requirements**

* Lighting device firmware **must** natively support the four standard HELP temporal patterns as defined in ISO/IEC PAS 86753\.  
* Upon receiving a setHelpState command, the device must immediately enter the alert state and continue the pattern indefinitely until it receives a cancelHelpState or clearState command.  
* If the device reboots or loses power while in a HELP state, it should attempt to resume the alert state upon power restoration for a period of up to 60 minutes.

#### **3.2 Certification Requirements ("HELP Certified")**

* **Colorimetric Accuracy:** Devices must reproduce the CIE 1931 xy coordinates for each HELP color within a tolerance of ΔE \< 3\.  
* **Temporal Accuracy:** Devices must reproduce the frequency, duty cycle, and waveform of each pattern within a 5% tolerance.  
* **Luminance:** Devices must be capable of achieving 100% of their rated lumen output during the brightest phase of the white strobe pattern.  
* **Reliability:** Devices must pass a 72-hour continuous activation test without deviation from the specified pattern.

### **4.0 Security & Anti-Misuse**

* **Authenticated Triggers:** All API calls to activate a HELP alert must originate from a platform-certified and authenticated device object. Unsolicited requests from unrecognized clients must be rejected.  
* **Rate Limiting:** Platforms should implement rate limiting on manual triggers (e.g., the Medical Emergency button) to prevent denial-of-service or prank-based attacks.  
* **Audit Logs:** A secure, user-accessible log of HELP activations and deactivations should be maintained for at least 30 days.
