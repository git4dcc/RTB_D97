# RTB_D97
[![Real-time Bus (RTB)](https://img.shields.io/badge/RTB_Project-FF6699)](https://www.rtb4dcc.de)
[![Kicad_Libs](https://img.shields.io/badge/Kicad_Libs-29C7FF)](https://github.com/git4dcc/RTB_SamacSys)
[![Apache License 2.0](https://img.shields.io/badge/license-Apache%20License%202.0-lightgray)](https://www.apache.org/licenses/LICENSE-2.0)

**Unleash your Homebrew DCC Function Decoder projects!**<br><br>
This repository provides a high-performance, **compiled firmware** optimized for the Microchip AVR64DA32 (see the pinout below!). I provide the digital brain—the rest is up to you. While essential support circuitry (power, dividers, level shifters) is required, this design choice is intentionally open, **inviting you** to innovate and customize your ultimate DCC decoder hardware. Scroll down for starter schematics and explore my other repos for more circuit ideas!

**User Guides**

- [User Guide - DE](https://rtb4dcc.de/rtb_fndecoder_Reference_de/)
- [User Guide - EN](https://rtb4dcc.de/rtb_fndecoder_Reference_en/)

<img src="supplemental/images/D97_main.jpg">

## Decoder firmware features
- **DCC**
  - DCC-A support (/w Preamble fingerprint)
  - DCC-R support
  - Service Mode Programming
  - Support of 'long 0000' programming address
- **Railcom**
  - Channel 1/2
  - jitter free
  - programmable TSS1, TSS2 timing
  - POM, xPOM
  - DYN: QoS, Track-Voltage, Temperatur, (and more)
- **I/O ports**
  - 10 AUX ports total (6 ports with 93kHz hardware PWM)
  - 32 LED ports
    - either (SR: 74HC595) or (WS: WS2811/WS2812) mode
  - One 10-bit analog output port (0-5V)
  - Two 12-bit analog input ports (0-5V)
  - SUSI port (5V)
  - Servo port
- **Automation**
  - light emulation (bulb, neon, mars, ditch, ...)
  - Port automation (head-/taillight, engine room, driver cabin, ...)
- **General**
  - buffer capacitor control
  - CPU heartbeat LED for status information
  - fast firmware update on main tracks via DCC-R
- **DCC protocol statistic reporting**
  - DCC bit timing
  - DCC frame rate

# Hardware
The software is compiled to run on a AVR64DA32 micro controller with the following pinout.

<img src="supplemental/images/D97_pinout.jpg">

| pin | label | direction | description |
| --- | --- | --- | --- |
| PA0 | F0r | output | Front light (rear) (/w hardware pwm) |
| PA1 | F0f | output | Front light (front) (/w hardware pwm) |
| PA2 | AUX1 | output | Auxiliary port 1 (/w hardware pwm) |
| PA3 | AUX2 | output | Auxiliary port 2 (/w hardware pwm) |
| PA4 | AUX3 | output | Auxiliary port 3 (/w hardware pwm) |
| PA5 | AUX4 | output | Auxiliary port 4 (/w hardware pwm) |
| PA6 | AUX5 | output | Auxiliary port 5 |
| PA7 | AUX6 | output | Auxiliary port 6 |
| PC0 | WS28xx | output | WS: DO / SR: data |
| PC1 | DCC-a | input | DCC input (left track) |
| PC2 | AUX7 | output | Auxiliary port 7 / SR: SHCP |
| PC3 | AUX8 | output | Auxiliary port 8 / SR: STCP |
| PD0 | uDCC-a | input | analog track voltage measure (left track) |
| PD1 | uDCC-b | input | analog track voltage measure (right track) |
| PD2 | iAUX | input | analog AUX current measure |
| PD3 | IN1 | input | analog input 1 |
| PD4 | IN2 | input | analog input 2 |
| PD5 | ACK | output | Service mode ACK current generator pin |
| PD6 | DAC_out | output | Analog output voltage |
| PD7 | CAP_ena | output | Buffer capacity control |
| PF0 | Servo_dat | output | Servo data |
| PF1 | Servo_pwr | output | Servo power control |
| PF2 | SUSI_sda | output | SUSI data |
| PF3 | SUSI_scl | output | SUSI clock |
| PF4 | Railcom | output | Railcom transmitter |
| PF5 | LED.hbt | output | Hearbeat LED |
| PF6 | DCC-b | input | DCC input (right track) |
| UPDI | UPDI | in/out | Programming pin |

## Kicad
[Schematic](doc/D97_schematic.pdf)

## Firmware
Initial firmware load must be done by using a UPDI programmer. Subsequent software updates can be done by using the RTB layout control infrastructure.

Filename structure: { **pcb** }{ **code** }{ **version** }.hex

Example: **D97F0001**.hex

|   | Description |
| --- | --- |
| **pcb** | Name of matching hardware (**D97**) |
| **code** | Type of code contained (**R**=rom, **B**=bootloader, **F**=flash, **U**=bld update, **P**=UPDI factory code) |
| **version** | Release version (**####**) |

[Firmware files](firmware)

## UPDI / Fuses
The fuse settings as well as the P-code (D97Pxxxx.hex) has to be installed by using UPDI.<br>

| Fuses Setting |
| --- |
|t.b.d|

# Example Hardware
| CPU only | /w Service Mode | /w Railcom |
| --- | --- | --- |
| <img src="supplemental/images/D97_proposal_1.jpg" width=310> | <img src="supplemental/images/D97_proposal_3.jpg" width=310> | <img src="supplemental/images/D97_proposal_4.jpg" width=310> |

| external LED ports |
| --- |
| <img src="supplemental/images/D97_proposal_5.jpg"> |
<br>

## Images
<img src="supplemental/images/D97_usecase1.jpg">


This project is intended for hobby use only and is distributed in accordance with the Apache License 2.0 agreement.
