# ARC-186 Radio Panel for DCS

**Last updated: October 30, 2026 at 4:04 AM MDT (America/Denver)**
<!-- Refresh this timestamp whenever this README changes; use the actual current America/Denver date and time with the correct MST/MDT abbreviation. -->

<p align="center">
  <img src="images/ARC-186_comm_vhf_panel.jpg" width="600" alt="ARC-186 COMM-VHF radio panel from PC Flights">
</p>

*Panel reference photo: [PC Flights](https://pcflights.com/a-10c-thunderbolt-warthog-comm-vhf-panel/).*

This project is planned as a physical ARC-186 COMM-VHF radio panel for my DCS A-10C II cockpit, with working controls and a display connected to DCS through DCS-BIOS.

## Project status

This repository is a placeholder while I work on my other radio projects. There is no firmware or finished hardware design available here yet, and I have not set a release date.

As development progresses, I will share build notes, schematics, firmware, parts lists, and photos here.

## Controller plan — separate Teensy 4.1 controllers

The plan is to use a **dedicated Teensy 4.1 for the ARC-186**, with another **Teensy 4.1 dedicated to the [ARC-164](https://github.com/dgdimick/ARC-164-DCS-Display)**. Each radio will have its own USB connection to DCS-BIOS and can be built and operated independently. This replaces the earlier shared-controller and Arduino Nano proposals.

The **Teensy 4.1 runs at 600 MHz**, compared with **16 MHz for the classic Arduino Uno R3, Mega 2560, and ATmega328P Nano** — **37.5 times the CPU clock frequency**. This provides processing headroom for display updates and controls; it is not a measured 37.5-times improvement in display refresh speed. See the [Teensy specifications](https://www.pjrc.com/store/teensy41.html) and [classic Arduino board comparison](https://github.com/dgdimick/ARC-210-DCS-Display/blob/master/Docs/Why-Teensy.md).

### Controller cost comparison

Reference prices checked **October 30, 2026**, in **USD per board, before shipping and tax**:

| Controller | Quantity for ARC-186 | Listed price | Supplier |
| --- | ---: | ---: | --- |
| Classic Arduino Nano, ATmega328P — considered, not selected | 1 | $25.70 | [DigiKey](https://www.digikey.com/en/products/detail/arduino/A000005/2638989) |
| Teensy 4.1 without Ethernet | 1 | $29.60 | [SparkFun](https://www.sparkfun.com/development-boards/microcontrollers/teensy/teensy-boards.html) |
| Teensy 4.1, standard, without soldered headers | 1 | $31.50 | [SparkFun](https://www.sparkfun.com/development-boards/microcontrollers/teensy/teensy-boards.html) |
| Teensy 4.1 with soldered headers | 1 | $35.95 | [SparkFun](https://www.sparkfun.com/development-boards/microcontrollers/teensy/teensy-boards.html) |

These are alternative controller options, **not quantities to purchase together**. Unsoldered versions may need separately purchased headers and sockets. Prices can change, and this table is a controller comparison rather than a complete panel build estimate.

The Teensy 4.1 without Ethernet costs only **$3.90 more than the genuine Nano** at these prices. That small difference makes the Teensy's additional I/O capacity, processing headroom, and consistency with the ARC-210 and ARC-164 projects worthwhile. Ethernet is not required for the planned USB DCS-BIOS connection.

### Pin budget and electrical plan

The preliminary ARC-186 budget is **19 signal pins**: 10 for five encoders, 3 analog inputs for two rotary-switch resistor ladders and volume, 3 for LOAD and a three-position squelch control, and 3 for a daisy-chained MAX7219 display arrangement. Against the Teensy 4.1's **42 readily accessible I/O pins**, that leaves **23 spare**. Analog inputs are included in those 42 pins; USB communication does not consume header GPIO pins. Encoder push switches and backlighting control are not included in this budget.

The earlier Nano pin assignments have been removed. **Teensy pin assignments will be established during the schematic design**; this is not a Nano pin-for-pin substitution. Teensy 4.1 uses **3.3 V logic and is not 5 V tolerant**. The proposed 5 V MAX7219 display drivers require suitable logic-level buffering, and the volume potentiometer and switch resistor ladders must use 3.3 V. See the [PJRC specifications](https://www.pjrc.com/store/teensy41.html).

Before finalizing the PCB, I will verify DCS-BIOS communication, all five encoders, rotary-switch analog readings, display updates, and the display power budget together. The display arrangement and pin budget remain proposed and untested. Firmware will map this single panel to the appropriate AM or FM radio.

## Why I keep using Teensy 4.1s

I’m using a Teensy 4.1 in each radio to keep the controller hardware and programming workflow consistent across the ARC-210, ARC-164, and ARC-186 projects. Each panel gets its own controller and USB connection, so it can be built and operated independently. Pin assignments and firmware will still be specific to each radio.

The Teensy 4.1 offers 42 readily accessible I/O pins and a 600 MHz processor, leaving room for controls, display updates, and future additions. Classic Arduino Uno and Mega boards run at 16 MHz. See [why I chose the Teensy 4.1](https://github.com/dgdimick/ARC-210-DCS-Display/blob/master/Docs/Why-Teensy.md) for the detailed comparison; clock speed alone does not determine display refresh performance.

I considered a classic Arduino Nano for the ARC-186, but the genuine Nano was listed at **$25.70** versus **$29.60** for the Teensy 4.1 without Ethernet—a difference of only **$3.90**, before shipping and tax, at the October 30, 2026 price check. For that small difference, I prefer the Teensy’s faster processor, extra capacity, and consistency across the radio projects. Its **600 MHz** CPU provides more processing headroom for display updates and controls than the classic Nano’s **16 MHz** CPU. The [ARC-186 controller comparison](https://github.com/dgdimick/ARC-186-DCS-Display#controller-cost-comparison) lists the options and supplier links. Ethernet is not needed for the planned USB DCS-BIOS connections.

## Other DCS aircraft using these radios

Beyond the A-10C and A-10C II, the following DCS aircraft use these radio types. This is a starting list for investigating future support, **not a list of aircraft currently supported by this project**.

| DCS aircraft | ARC-164 | ARC-186 |
| --- | :---: | :---: |
| F-16C Viper | Yes | — |
| F-5E Tiger II | Yes | — |
| F-4E Phantom II | Yes | — |
| C-101EB | Yes | — |
| AH-64D Apache | Yes | Yes |
| CH-47F Chinook | Yes | Yes |

Sources: [F-16C manual](https://www.digitalcombatsimulator.com/upload/iblock/3dc/5p9ejw7gi488n9zd15csrxxs8os2dflk/DCS_F-16C_Early_Access_Guide_EN.pdf), [F-5E manual](https://www.digitalcombatsimulator.com/upload/iblock/528/DCS%20F-5%D0%95-3%20Flight%20Manual_ENG.pdf), [F-4E DCS-BIOS device list](https://github.com/DCS-Skunkworks/dcs-bios/issues/584), [C-101EB manual](https://shared.akamai.steamstatic.com/store_item_assets/steam/apps/316966/manuals/DCS_C-101EB_Flight_Manual_EN.pdf?t=1727212356), [AH-64D manual](https://www.digitalcombatsimulator.ru/upload/iblock/c22/hyhtbs5kqjyjauapanut3az7bbs3p3b1/DCS_AH-64D_Quick_Start_Manual_EN.pdf), and [ED’s CH-47F explanation](https://forum.dcs.world/topic/358422-missing-radio/).

**Support for each additional aircraft would require separate DCS-BIOS mappings, firmware integration, and testing.** Using the same radio model does not make the A-10 mappings compatible with another aircraft. Available inputs, display outputs, control behavior, and DCS-BIOS coverage must be checked for each module.

The AH-64D controls these radios through its integrated avionics. The CH-47F controls its ARC-164 through the CDU/MFDs and has an ARC-186 backup control head, so its cockpit interface differs from the A-10-style panels. No additional-aircraft support or release date is promised.

## Related projects

- [ARC-210 DCS Display](https://github.com/dgdimick/ARC-210-DCS-Display)
- [ARC-164 DCS Display](https://github.com/dgdimick/ARC-164-DCS-Display)

## Questions and community builds

Visit [GitHub Discussions](https://github.com/dgdimick/ARC-186-DCS-Display/discussions) to ask questions, share ideas, and post photos of your build. Whether you’re planning your panel or already working on it, you’re welcome to join in!

## PC Flights affiliation

I am not affiliated with PC Flights. I simply chose to use their panels for my own cockpit projects.
