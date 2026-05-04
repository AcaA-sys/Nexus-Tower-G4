
## Communication & Intelligence (Nexus-CAN FD)

Nexus-Tower-G4 acts as a specialized high-speed node in the Nexus Ecosystem, managing toolhead motion and precision sensing. It communicates with the Master (H723) via the **Bus B (Instrumental)**.

### Toolhead Capabilities:
- **Multi-Axis Control:** Local management of 6 auxiliary axes (Z-lift, Dual Nozzle Rotation, Tool Changer, etc.).
- **Vibration Analytics:** High-precision integration with **ADXL355** (20-bit) for 5-8 micron motion stability.
- **Black Box Logging:** On-board **W25Q128 SPI Flash** for high-speed vibration data storage (up to 4000Hz) to bypass CAN FD 5Mbps bandwidth limits.
- **Thermal Correction:** Real-time monitoring via **DS18B20** for hardware thermal expansion compensation.

### Protocol Summary (Bus B):

| ID | Function | Data Type |
| :--- | :--- | :--- |
| **0x120** | Accel Stream | 20-bit XYZ (Real-time) |
| **0x310** | Axis Control | Target Pos/Vel for 6 Axes |
| **0x311** | Feedback | Vacuum (ADS1115) + Status |
| **0x720** | Data Dump | Black Box Flash retrieval |

> **Note:** The physical layer is restricted to **5 Mbps** by the TD541SCANFD transceiver. High-bandwidth acceleration logs are retrieved via Service Mode when the machine is idle.
