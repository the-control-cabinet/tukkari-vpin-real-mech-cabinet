# 06 · Software, DOF and Configuration

[← Back to README](../README.md)

## Versions

| Component | Version | Notes |
|---|---|---|
| Visual Pinball X (VPX) | 10.8, 64-bit (where required) | |
| VPinMAME | ⟨record⟩ | |
| B2S Server | ⟨record⟩ | DLL registered after install |
| DirectOutput Framework (DOF) | ⟨record⟩ | Config from the DOF Config Tool (`directoutputconfig30.ini` / `90.ini`) |
| Dude's Cab firmware | ⟨record⟩ | |
| Dude's Cab Configurator | ⟨record⟩ | |
| PinUp Popper (Baller) | planned | Moves across with the dedicated PC |
| ESPHome (rail monitor) | 2026.9.x | Same version as the rest of the ESP32 fleet |
| Home Assistant | 2026.x | |

## Arnoz board facts that matter for configuration

| Item | Detail |
|---|---|
| Bunny | Walter Driver + 2 × MOS8 on one PCB: **16 PWM MOSFET outputs**, up to 8 A each, **40 A total**, toys 0-48 V, opto-isolated, a 5×20 mm fuse and test LED per output |
| Bunny power | Needs its own **12 V logic supply** plus heavy ground returns; toy positives go straight to their rail, and the Bunny switches the negative |
| Expansion | A standalone MOS8 can't connect to a Dude's Cab; it needs a Walter. Up to 8 Walters/Bunnies per Dude's Cab |
| Max Value | 0-255 PWM ceiling per output |
| **General Power ("Masta Powaa")** | Scales **every** Max Value and fall-off value on the board. **Left at default** here |
| PWM frequency | Adjustable per board (raise it above ~20 kHz to remove coil or motor whine). **Left at default** here |
| Per-output logic | Flipper logic (kick then hold), chime logic, fall-off delay/value, security delay, Night Mode sensitivity |
| Applying changes | **Send Config** (live), then **Save to Memory** (survives a reboot) |
| Addressable LEDs | Set up only in the Configurator's Addressable LEDs tab. With an MX Donny present there must be **no `cabinet.xml`**. Arrangement maps the physical LED order to DOF's logical order |

## VPX audio and DOF settings (as configured)

| Setting | Value | Effect |
|---|---|---|
| VPX → Keys, Nudge & DOF → **Flippers** | **DOF only** | Real flipper coils make the sound; VPX doesn't play its samples |
| **Contactors** (bumpers + slings) | **DOF only** | Real coils make the sound |
| Audio | 7.1 Surround Sound Feedback (enhanced) | Ball roll and positional sound go to the SSF exciters |
| Targets / Drop targets | (reference) By default DOF fires them as short bumper pulses, which isn't realistic, because real stand-up and drop targets don't fire a coil on a hit. Options: lower their intensity, or leave their VPX sound on | |
| **Night Mode** | Turns off outputs flagged "Sensitive to Night Mode" | ⚠️ Doesn't change VPX, so with DOF-only set there's **no** flipper or bumper sound at all. Fix: switch Flippers/Contactors to Sound/Both when Night Mode is on, e.g. a batch file using IniMod to edit `VPinballX.ini` (roadmap) |

## DOF mapping: expanded 10-output profile (current)

Each physical coil takes every DOF toy that a table might call for that position, combined in the DOF Config Tool's **Combine Toys** tab, so old (8-bumper) and modern (10-bumper) tables both fire something.

| Physical coil | Board | DOF toys combined |
|---|---|---|
| Flipper Left / Right | Bunny 1 | Flipper Left / Flipper Right |
| Sling Left / Right | Bunny 1 | Slingshot Left / Slingshot Right |
| Bumper Middle Left | Bunny 1 | 8 Bumper Left + 10 Bumper Middle Left |
| Bumper Middle Centre | Bunny 1 | 8 Bumper Center + 10 Bumper Middle Center |
| Bumper Middle Right | Bunny 1 | 8 Bumper Right + 10 Bumper Middle Right |
| Bumper Rear Left | Bunny 2 | 10 Bumper Back Left |
| Bumper Rear Centre | Bunny 2 | 10 Bumper Back Center + 8 Bumper Back |
| Bumper Rear Right | Bunny 2 | 10 Bumper Back Right |

Notes:
- Flippers and slings have no 8/10 variants; only the bumper positions differ. "Back" and "rear" are the same row, and there's only one back-centre toy.
- **Mono vs Mono:Feedback:** use Mono:Feedback for the knocker and other loud contactors; Mono for everything else.
- **Topper Bell / Repeating Bell:** tables that only call Topper Bell can drive a continuously ringing bell (such as the fire-alarm bell) by combining it with Repeating Bell. Hellball toys are effectively unused by published tables.
- **How to Play / Genre:** front-end button LEDs only; leave them unassigned unless those buttons are lit.

## ARGB toys: DOF combinations (reference)

| Device | DOF toys combined |
|---|---|
| Left side strip + left flipper button | PF Left Flashers MX + PF Left Effects MX + Flipper Button MX |
| Right side strip + right flipper button | PF Right Flashers MX + PF Right Effects MX + Flipper Button MX |
| Left / right magna save | Left / Right MagnaSave MX |
| HD matrix | PF Back Flashers MX + PF Back Effects MX (+ Strobe optional) |
| Flashers | PF Back Flashers MX (classic 5-flasher bar). Individual flashers can also be separate LED strips on the same Donny port, each with its own DOF output, for independent effects |
| Speaker rings (256 LEDs) | PF Back Effects MX + PF Back Flashers MX |
| Undercab strips | RGB Undercab Complex MX |

Exact live mappings will come with the DOF config files.

## MX (addressable) flasher effects: command syntax
Order: **trigger → colour → effect → parameters**, separated by spaces; multiple commands on a toy are separated by `/`.

| Example | Meaning |
|---|---|
| `L78 Red Blink fu300 fd300` | Lamp 78 triggers a red blink with 300 ms fade-up and 300 ms fade-down |
| `L78 Blue Blink fu150 fd100` | Fast strobe |
| `L78 White Blink fu800 fd1200` | Slow pulse |
| `L78 Green Blink fu300 fd300 AL0 AT0 AW4 AH100` | Limited to a 4-LED area (left/top 0, width 4, full height) |

The MX toy needs a combo set to **RGB Addressable** with the correct start port. Regenerate the config files and restart DOF/VPX after changes.

## DOF and custom toys: full set-up coming
The complete DOF set-up will be documented here, with the config files in [`config/dof/`](../config/dof/README.md):
- every toy's output mapping
- custom toy definitions
- hand-edited `.ini` entries
- the Configurator export

---

## Software Stack

### Install order (tested path for laptop proof-of-concept)
1. VPinMAME
2. Visual Pinball X (10.8 64-bit for tables that require it)
3. B2S Server (register the DLL; screenres editor appears during setup)
4. DirectOutput Framework (DOF) — 32-bit registers cleanly; 64-bit may require admin / specific order
5. Dude’s Cab Configurator
6. Tables + ROMs as needed

### Notes
- DOF Config Tool (web) generates `directoutputconfig30.ini`, `directoutputconfig90.ini`, etc. Place in the DirectOutput folder (not only the Config subfolder — both locations discussed).
- Cabinet.xml not always generated for pure Donny/MX setups.
- VPX key config only exposes buttons 1–24; higher button numbers from Dude’s Cab require mapping care or reassignment.
- DOF test table and forced-white commands in `directoutputconfig30.ini` used for ARGB verification.

### Full cabinet
PinUp Popper Baller installer planned once the dedicated PC and screens are installed. Laptop USB connection to Dude’s Cab sufficient for toy and ARGB proof-of-concept.

---

## DOF and Dude’s Cab — Configuration Behaviour and Test Methods

### Dude’s Cab Configurator
- Bunny ports are assigned devices and given logic type (normal, flipper, etc.).  
- FallOff Value, FallOff Delay and (when visible) Security Delay are set per toy.  
- Matrix is created as a single 96 × 16 definition; splits are auto-assigned to additional Donny ports.  
- Built-in LED tests (RGB, Colours, Laser) produce only brief pulses — insufficient for sustained white current-draw or visual checks.

### DOF integration
- Web-based DOF Config Tool generates directoutputconfig30.ini and directoutputconfig90.ini (and related files).  
- These files belong in the DirectOutput folder; some users also keep copies in the Config sub-folder. Cabinet.xml is not always produced for pure Donny/MX setups.  
- Blower was mapped to the Fan toy or to a custom output depending on whether cabinet fans were also on a Bunny port. Cabinet fans were ultimately preferred on motherboard PWM so games would not drive them.  
- Button numbers above 24 (Dude’s Cab supports higher) do not appear in the VPX key-config drop-down (limited to 1–24). Mapping must be handled by assigning the physical button to a Dude’s Cab input that VPX can see, or by accepting the limitation.

### Sustained white test method that worked
Edit the relevant table section inside directoutputconfig30.ini and add permanent ON White triggers with area parameters matching the Donny channels / matrix splits, for example:

```
ON White AH100 AL0 AT0 AW100
```

Load any table whose cGameName matches the DOF profile (or the DOF test table). Mechanical toys continue to respond to their normal events; the lighting is forced on. Colour balance on “white” can appear cool/blue depending on LED bin and power; this is normal.

### Known edge case
An abrupt exit from VPX into PinUp Popper can leave DOF outputs asserted. Dude’s Cab fall-off and security-delay settings are the mitigation. Reports exist of stuck coils even with FallOff Value = 0 and a 35 ms delay; the PTC + port fuse remain the hardware backstop.

---

## Example DOF forced-white fragment (for testing)

Place in directoutputconfig30.ini under the appropriate table section (e.g. dof_test).

```
dof_test,S0 FF FF FF/S0 FF FF FF,S0 FF FF FF,... (mechanical)
,E122 Green 1500 AL0 AT0/E120 Red 1500 AL0 AT0/E123 Blue 1500 AL0 AT0,...
```

For sustained full white on MX/ARGB areas use permanent ON triggers with area parameters, for example:

```
ON White AH100 AL0 AT0 AW100
```

Adjust area codes (AH, AL, AT, AW, etc.) to match the Donny channel / matrix splits defined in Dude’s Cab.  
Test with the DOF test table or any table whose cGameName matches the profile.  
Mechanical toys continue to respond to their normal triggers; the white lines force the lighting.
