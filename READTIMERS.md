<h1 align="center">8051 Timers</h1>

## Introduction

The 8051 microcontroller has two built-in timers/counters: Timer 0 and Timer 1 each 16 bit. These are used to measure time intervals, generate delays, or count external events. Timers can operate in timer mode (counts machine cycles) or counter mode (counts external pulses).

Timers in 8051 are 16-bit registers, meaning they can count from 0x0000 to 0xFFFF. They are widely used for tasks such as delay generation, event counting, pulse width modulation (PWM), and serial communication timing

Each timer register divided into two parts **Timer High** and **Timer Low**, Timer 0 has **TL0 and TH0** whereas Timer 1 has **TL1 and TH1**
## Timer Modes

TMOD register is a 8 bit regoster which is used to select a mode for timers
| Mode       | Bit Length         | Description                                                        |
| ---------- | ------------------ | ------------------------------------------------------------------ |
| **Mode 0** | 13-bit             | Timer counts 13 bits: TLx (8-bit) + upper 5 bits of THx            |
| **Mode 1** | 16-bit             | Full 16-bit timer: TLx + THx                                       |
| **Mode 2** | 8-bit auto-reload  | TLx counts 8 bits; on overflow, TLx reloads from THx automatically |
| **Mode 3** | Split Timer 0 only | Timer 0 is split into two 8-bit timers: TL0 and TH0                |

**MODE 1** is commenly used adn we'll also use **MODE 1**
## TCON Register

The TCON (Timer Control) register is an **8-bit special function register** that controls the timers and external interrupts in the 8051. It also stores the overflow flags and external interrupt flags.

| Bit | Name    | Function                                                |
| --- | ------- | ------------------------------------------------------- |
| 7   | **TF1** | Timer 1 overflow flag (set when Timer 1 overflows)      |
| 6   | **TR1** | Timer 1 run control (1 = Timer 1 runs, 0 = stops)       |
| 5   | **TF0** | Timer 0 overflow flag (set when Timer 0 overflows)      |
| 4   | **TR0** | Timer 0 run control (1 = Timer 0 runs, 0 = stops)       |
| 3   | **IE1** | External Interrupt 1 edge flag                          |
| 2   | **IT1** | External Interrupt 1 type control (1 = edge, 0 = level) |
| 1   | **IE0** | External Interrupt 0 edge flag                          |
| 0   | **IT0** | External Interrupt 0 type control (1 = edge, 0 = level) |









