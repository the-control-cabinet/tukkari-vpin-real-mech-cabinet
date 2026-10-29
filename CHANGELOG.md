# Changelog

## 2026-10-29
- Diagram PDFs: co-author Martafix's email address redacted (text removed, not just covered), PDF metadata cleared, previews regenerated. Credit to Martafix kept. Repository history squashed so earlier versions no longer contain it.

## [2.4.1] - 2026-10-27
- Diagram PDFs: the author's personal email address redacted (text removed, not just covered), PDF metadata cleared, previews regenerated.

## [2.4.0] - 2026-10-27: inrush and hold corrections
- **Inrush (agreed wording):** coils pull ≈V/R at full voltage (≈6 A at 24 V; the same surge reaches 20 A+ on real machines at 50-70 V). The 15-30 A rail spikes also include the electrical and magnetic switching spikes documented when coils are pulsed and PWM'd. A shunt + scope capture is planned to separate them. References carry their voltage context.
- **Hold current:** the ≈2 A at 2 % reading was wrong. Re-test shows ≈0.1 A, so Dude's Cab PWM works as intended. Removed the 16 W heating analysis, the "non-linear fall-off" hypotheses and the bell-shaped decay description.

## [2.3.0] - 2026-10-27: corrections
- **Inrush:** the 15-30 A spikes and ≈7.2 A smoothed readings are genuine coil inrush on the 24 V rail, consistent with documented pinball behaviour when pulsing/PWMing coils. The earlier calibration-artefact and concurrent-coil explanations are removed. Real-machine references added (Pinside, Mission Pinball Framework).
- **5 V load:** gameplay draw is well below the 30 A ANL (effects and brightness settings, no sustained full white). Removed the 25-40 A estimate and the "confirm against 30 A" item.

## [2.2.0] - 2026-10-27: confirmed I/O, allocations and parts list
### Changed
- Bunny 1 and Bunny 2 outputs set from the confirmed I/O map (gear motor on Bunny 2 port 9; gear motor 2 planned on port 10).
- MX Donny: ports 6-8 HD matrix; 1-5 button/side/undercab chains, flashers, ARGB fans, speaker rings.
- Flashers: 19 MX flashers × 4 LEDs (5 commissioned, 14 for a custom topper).
- La Nettoyeuse on shaker, repeating bell, topper blower and gear motor (+ gear motor 2); none on solenoid coils. Removed the gear-motor capacitor review item.
- Shaker identified as the Stern Spike kit by PinSound; cabinet identified as Tukkari widebody.
### Added
- README photo gallery (all 12 build photos), wiring-diagram previews, and a "Still to add" list (STLs, DOF configs, custom mechanical and ARGB toys, MX/HD effect groups).
- `hardware/3d-printed-parts.md` index of STLs with links (tracking parameters removed).
- Voltboard output allocation; inputs (button boards, Brain undercab buttons, coin door interlock on DOOR); LM2577 PC-LED circuit.
- Points list rebuilt for all 32 Bunny outputs with rail, fuse, PTC, suppression and DOF notes.
- Lighting rules (chain order, LED-count bleed, star power/series data, dual-end injection), ARGB DOF combinations, wiring conventions, SSF hardware (second BST-1 planned).
- Full parts list (`hardware/parts-list.xlsx` + `.md`) with installed/planned status; old parts-list notes removed.

## [2.1.0] - 2026-10-26: merged the Grok handover documents
### Changed
- **Flipper as-built wiring:** +24 V on the **right** lug, Bunny on the **middle**, left disconnected, diode band on the right lug. The diagrams show the textbook +24 V-on-middle orientation; both are valid with one winding.
- **Fall-off wording:** 10 % is the setting everywhere; 2 % appears only as a test.
- **Fuses:** all coils on 2.5 A SB (Bunny 2 changed from 4 A since the photo); RUEF160 on all 10 playfield coils; knocker, chimes and shell bell without RUEF160 (outstanding). 12 V inline fuse 20 A; 5 V 30 A **ANL**.
- "Inrush" explained as pull-in current ≈ V/R. Bumper readings above V/R are flagged as clamp scaling/noise, and a calibration step is added.
### Added
- Fuse and PTC trial history: 2 A vs 2.5 A SB; RUEF250 rejected; RUEF185 fallback; RUEF160 chosen.
- PSU terminal strategy and wire-table guidance; distributed grounding; audio PSU isolated by design; the **unprotected 5 V direct-Voltboard leg** (safety and roadmap).
- Fliptronics EOS explanation; the flipper measurement lesson (diodes lifted).
- Arnoz board facts (Bunny limits, Max Value, General Power/"Masta Powaa", PWM frequency, Send Config/Save to Memory, no `cabinet.xml` with an MX Donny).
- VPX DOF-only settings, the Night Mode limitation and fix, the expanded 10-output DOF combo table, Mono:Feedback, Topper/Repeating Bell, MX flasher command syntax.
- Fault log: the undercab strip reversal (resolved via Arrangement), reversed diode, ARGB fan pinout, cut-strip LED count.
- PinSound shaker via a 7 V step-down; 12 V truck-fan topper blower; amps confirmed; completed build items; smoked-tape strip tint.

## [2.0.0] - 2026-10-26: restructure and corrections
### Changed
- Docs merged from 19 into 12 numbered documents, each value now in one place. README rewritten to be self-contained.
- **Flipper wiring corrected:** +24 V on the middle lug, Bunny on the right lug (power winding only), left lug disconnected. The earlier text described +24 V on the right and middle lugs.
- **Flipper fall-off clarified:** 10 % configured; holds down to 2 %; drops at 1 %.
- **5 V inline fuse:** reduced from 60 A to **30 A**.
- RUEF160 results recorded: under 10 s trip on a stuck coil, no false trips in play.
- Removed the incorrect statement that ESPHome wasn't used.
- **La Nettoyeuse corrected:** it's fitted to the topper blower, not the knocker. No coil has one; coils use a 1N4007 only. Photo renamed `topper-blower-la-nettoyeuse.jpg`.
- YouTube channel links switched to the channel-ID URL (the @handle URL 404s from GitHub).
- Diagram files renamed to kebab-case, with PNG previews; credited co-author Martafix.
### Added
- 07 Instrumentation: the ESP32 rail monitor (4 Hall clamps + DS18B20, BLE proxy), signal processing, YAML pattern, HA dashboard card, and the flipper hold test (≈6 A inrush, ≈2 A sustained at 2 %) with analysis.
- 08 Internal gameplay camera plan (Raspberry Pi + camera, HDMI to a projector as the 4th screen).
- 10 Safety (mains and earthing, fusing principles, protection layers, polarity, thermal, the 24 V audio fuse gap).
- Power budget, versions table, draft I/O points list (`data/points-list.csv`), test record, config folders for DOF, ESPHome and HA.
- Decision log rows: rail monitoring, BLE proxy, camera; 24 V audio marked for review.

## [1.0.0] - 2026-10
- Initial documentation drafted with Grok: architecture, power, Bunny/Donny, HD matrix, toys and coil protection, audio, software and DOF notes, troubleshooting, videos, diagrams, photos.
