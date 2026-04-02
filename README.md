Work in Progress. 

While the Master H7 handles trajectory planning, the Nexus-Tower node offloads local head functions via CAN FD:
- MCU: STM32G431 (Advanced Analog & FDCAN).
- Option 1 Axis Z: Integrated FOC/Servo support for soft-landing placement. + Axes C1/C2: Dual TMC2209 for NEMA 8/11 nozzles (UART control).
- Option 1 Motion: 3x Stepper (Z, C1, C2) via TMC2209.
- Pneumatics: 4x Valve outputs + 2x High-speed Analog Vacuum sensing (ADC over CAN).
- IO: 3x Endstops + 1x PWM Light control.

