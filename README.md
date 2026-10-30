# ARC-186 Radio Panel for DCS

<p align="center">
  <img src="images/ARC-186_comm_vhf_panel.jpg" width="600" alt="ARC-186 COMM-VHF radio panel from PC Flights">
</p>

*Panel reference photo: [PC Flights](https://pcflights.com/a-10c-thunderbolt-warthog-comm-vhf-panel/).*

This project is planned as a physical ARC-186 COMM-VHF radio panel for my DCS A-10C II cockpit, with working controls and a display connected to DCS through DCS-BIOS.

## Project status

This repository is a placeholder while I work on my other radio projects. There is no firmware or finished hardware design available here yet, and I have not set a release date.

As development progresses, I will share build notes, schematics, firmware, parts lists, and photos here.

## Controller plan — separate controllers

The plan is to use a **classic 5 V Arduino Nano with an ATmega328P for the ARC-186**, while keeping the **Teensy 4.1 dedicated to the [ARC-164](https://github.com/dgdimick/ARC-164-DCS-Display)**. Each radio will have its own USB connection to DCS-BIOS and can be built and operated independently. This replaces the earlier shared-controller proposal.

The Nano pin budget fits one ARC-186 panel using four frequency encoders, one preset-channel encoder, resistor ladders for the two rotary switches, and a daisy-chained MAX7219 LED display arrangement. The count is **19 signal pins, leaving one spare** after reserving D0/D1 for serial communication. Power and ground connections are additional to this signal-pin count.

### Proposed Nano pin assignments

These assignments apply to the **classic ATmega328P Nano**, not other Nano-family boards. See the [official Nano pinout](https://docs.arduino.cc/resources/pinouts/A000005-full-pinout.pdf).

| Function | Nano pins | Connection |
| --- | --- | --- |
| Frequency encoder 1 | D2, D3 | A/B signals |
| Frequency encoder 2 | D4, D5 | A/B signals |
| Frequency encoder 3 | D6, D7 | A/B signals |
| Frequency encoder 4 | D8, D9 | A/B signals |
| Preset-channel encoder | A0, A1 | Used as digital inputs for A/B signals |
| Display LOAD/CS | D10 | Shared MAX7219 chain |
| Display data | D11 | MAX7219 DIN |
| LOAD button | D12 | Digital input |
| Display clock | D13 | MAX7219 CLK |
| Squelch control | A2, A3 | Digital inputs; reserves support for three positions |
| Volume potentiometer | A4 | Analog input |
| **Spare** | **A5** | Available for a future function |
| Mode rotary-switch resistor ladder | A6 | Analog-only input |
| Frequency/emergency rotary-switch resistor ladder | A7 | Analog-only input |
| DCS-BIOS serial — reserved | D0/RX, D1/TX | Leave free of panel controls for USB serial communication |

A6 and A7 are analog-only pins and are allocated to resistor ladders accordingly. Multiple MAX7219 drivers can use the same three-wire chain. Encoder push switches and backlighting control are **not included** in this budget.

The controller choice is the current plan; the pin assignments and MAX7219 display arrangement remain **proposed and untested**. Before finalizing the PCB, I will verify DCS-BIOS communication, all five encoders, rotary-switch analog readings, display updates, and the display power budget together. Firmware will map this single panel to the appropriate AM or FM radio.

## Related projects

- [ARC-210 DCS Display](https://github.com/dgdimick/ARC-210-DCS-Display)
- [ARC-164 DCS Display](https://github.com/dgdimick/ARC-164-DCS-Display)

## Questions and community builds

Visit [GitHub Discussions](https://github.com/dgdimick/ARC-186-DCS-Display/discussions) to ask questions, share ideas, and post photos of your build. Whether you’re planning your panel or already working on it, you’re welcome to join in!

## PC Flights affiliation

I am not affiliated with PC Flights. I simply chose to use their panels for my own cockpit projects.
