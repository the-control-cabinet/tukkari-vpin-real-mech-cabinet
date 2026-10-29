# Decision Log

[← Back to README](../README.md)

| Topic | Decision | Why | Status |
|-------|----------|-----|--------|
| Matrix Donny ports | 3 ports, paired chaining | Frame rate vs port count; 6 ports unnecessary | Done |
| Matrix orientation | Connectors at bottom (player view) | Wires exit upward into cabinet | Done |
| Flipper wiring | +24 V on **right** lug, Bunny on **middle** lug (power winding only), left lug (hold) disconnected, diode band on the right lug, software PWM hold | Single port; Fliptronics EOS is NO gold (feedback only); measured 4 Ω power / 122 Ω hold. Polarity irrelevant with one winding (diagrams show middle-+24 V) | Done |
| Coil protection | 10 % fall-off + 2.5 A SB on every coil + RUEF160 on all 10 playfield coils + 1N4007 | 2 A SB too fast (under 0.5 s), 2.5 A SB too slow (over 30 s) on a stuck coil; RUEF250 didn't trip in 15 s; RUEF160 under 10 s with no false trips | Done |
| RUEF160 on knocker, chimes, shell bell | Not fitted yet | Lower duty than the playfield coils; under consideration | **Outstanding** |
| 12 V inline fuse | 20 A | Below both the 12 AWG feed (about 16-25 A) and the 25 A block | Done |
| 5 V direct-Voltboard leg | Not separately fused | Identified gap: the 30 A ANL can't protect a lighter leg | **Fix on roadmap** |
| Audio PSU ground | Negative isolated from the common ground | Keeps coil return currents out of the audio reference | Done |
| Grounding strategy | Distributed: bond block plus local returns; Bunny grounds split 24 V / 12 V | Avoids single-terminal bottlenecks; central bus possible later | Done |
| Shaker | PinSound shaker via a 7 V step-down (kept), Bunny PWM | Step-down kept rather than relying on Max Value/General Power | Done |
| DOF mapping | Expanded 10-output profile with 8/10-bumper combos | Rear bumpers fitted; covers old and modern tables | Done |
| VPX sound | Flippers and Contactors on DOF only; SSF for everything else | Real coils provide the mechanical sound | Done |
| Night Mode | Mech off; VPX sound fallback still needed | DOF-only leaves no sound when the mech is silenced | **Outstanding** |
| Undercab strip direction | Reversed with Arrangement in the Configurator | Data injected from the rear; matches the playfield strips | Done |
| Strip tint | Smoked-tint LED strip; clear covers | Tint film impractical | Done |
| Bumper LEDs | Parallel at coil after PTC, 470 Ω + optional cap | No new long runs; PTC protects LED leg | Planned |
| 24 V audio | Direct from PSU terminals, no TB/fuse | Space; short single runs; avoided wiring in fuse holders. **Should ideally be fused**, see roadmap | Done (review) |
| Terminal blocks | Move toward 25 A; evaluate dual backhaul | 15 A blocks marginal on concurrent peaks | In progress |
| Donny port freeing | Combine undercab with playfield side strips | Needed two ports for matrix; rejected combining L/R sides | Done |
| Reference ground | Bond at load end only | Interference reduction without loop | Recommended |
| La Nettoyeuse | On shaker, repeating bell, topper blower, gear motor (+ gear motor 2); none on solenoid coils | Motors and bells need noise filtering; coils need flyback suppression only | Done |
| DOF white test | Direct .ini permanent ON White | Configurator pulses too short | Used |
| Backglass blackout | Spray paint rear side | Tint film impractical | Done |
| Gear motor intensity | Single Bunny PWM port + DOF intensity | Configurator Max Value is ceiling; real-time intensity supported. Earlier 3-port advice superseded | Done |
| Gear motor location | Primary UR, second ML planned (Bunny 2 port 10) | ~80 % of gear tables are upper-right | Primary done; second planned |
| SSF mapping | Front=backbox, Surround=rear exciters, Back=front exciters | Standard 7.1 SSF orientation | Done |
| MX Donny / MX button | Closed — loose playfield LED strip connection blew the MX button board | Not a failed Donny port. Connection fixed, button replaced | Closed |
| Bunny fall-off | 35 ms / 0 % on pulse toys; 35 ms / **10 %** on flippers, security delay about 60 s | Real-mech protection. 2 % tested (still holds at ≈0.1 A) but never used | Done |
| Inline fuses | 5 V (**30 A ANL**, was 60 A), 12 V (**20 A**), 24 V mech (30 A) yes; 24 V audio no | PSU limp mode insufficient for multi-branch shorts; audio skipped to avoid wiring holders into short single runs, which ideally it should have | Done (audio fuses on roadmap) |
| Rail monitoring | ESP32 with four clamp-on Hall sensors (one per PSU) plus a DS18B20 | Measure pull-in and sustained current per rail; verify protection settings with data; ≈6 A inrush per coil and 15-30 A rail spikes captured | Done |
| BLE proxy on the VPin ESP32 | Kept on | Spare capacity; adds Bluetooth coverage in that room | Done |
| Gameplay camera | Raspberry Pi + camera, HDMI to a 4th screen (projector) | Direct HDMI output, frame rate and latency; ESP32-S3-CAM can't output HDMI | Planned |

| Bunny I/O | Bunny 1: flippers, slings, middle bumpers, knocker, shaker, LEDs, bell, beacons, blower, strobes. Bunny 2: shell bells, chimes, rear bumpers, gear motors | Coils grouped by function; Bunny 2 added for chimes, bells and rear bumpers | Done |
| Donny | Ports 6-8 HD matrix; 1-5 buttons/side/undercab chains, flashers, fans, rings | Matrix paired across 3 ports for frame rate | Done |
| Coin door interlock | Brain DOOR terminal (pole 1); interior LEDs (pole 2) | Frees a Bunny port for the interior LEDs | Done |
| PC power / undercab button LEDs | Motherboard PWR_LED → LM2577 boost → 12 V | Lit whenever the PC is on; no Bunny port needed | Done |
| Flashers | 19 MX flashers × 4 LEDs (5 commissioned, 14 for custom topper) | Custom topper in progress | In progress |
| Bass shakers | 1 × BST-1; second planned on the spare rear-SSF amp channel | Use spare amp capacity | Planned |

Add rows when a choice is locked or revised. Include measured numbers where they drove the decision.
