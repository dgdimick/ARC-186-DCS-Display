# ARC-186 Radio Panel for DCS

<p align="center">
  <img src="images/ARC-186_comm_vhf_panel.jpg" width="600" alt="ARC-186 COMM-VHF radio panel from PC Flights">
</p>

*Panel reference photo: [PC Flights](https://pcflights.com/a-10c-thunderbolt-warthog-comm-vhf-panel/).*

This project is planned as a physical ARC-186 COMM-VHF radio panel for my DCS A-10C II cockpit, with working controls and a display connected to DCS through DCS-BIOS.

## Project status

This repository is a placeholder while I work on my other radio projects. There is no firmware or finished hardware design available here yet, and I have not set a release date.

As development progresses, I will share build notes, schematics, firmware, parts lists, and photos here.

## One controller or two?

I’m considering two ways to connect the ARC-186 and [ARC-164](https://github.com/dgdimick/ARC-164-DCS-Display):

- **One shared controller:** Use the Teensy inside the ARC-164 to handle both radios through DCS-BIOS, with a plug-in cable connecting the ARC-186 to it. This could reduce the number of controllers and USB connections needed and help keep the combined build cost down.
- **Separate controllers:** Give each radio its own controller and USB connection. This would let you build and use either radio independently, without needing the other panel, and keep each radio’s wiring and firmware separate.

My aim is to document both arrangements so builders can choose what suits their cockpit. I’m still investigating the available pins, display connections, cable and connector requirements, and firmware for the shared-controller option. Neither arrangement is finalized yet, and any cost savings remain to be confirmed. I’ll share the details here as the designs develop.

## Related projects

- [ARC-210 DCS Display](https://github.com/dgdimick/ARC-210-DCS-Display)
- [ARC-164 DCS Display](https://github.com/dgdimick/ARC-164-DCS-Display)

## Questions and community builds

Visit [GitHub Discussions](https://github.com/dgdimick/ARC-186-DCS-Display/discussions) to ask questions, share ideas, and post photos of your build. Whether you’re planning your panel or already working on it, you’re welcome to join in!

## PC Flights affiliation

I am not affiliated with PC Flights. I simply chose to use their panels for my own cockpit projects.
