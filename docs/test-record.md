# Test Record

[← Back to README](../README.md)

| # | Test | Method | Result | Status |
|---|---|---|---|---|
| 1 | FL-11629 coil identification | Diodes lifted, meter zeroed, all three lug pairs | L–M 122 Ω (hold), M–R 4 Ω (power), L–R 126 Ω | ✅ |
| 2 | Flipper hold threshold | Lower the Dude's Cab fall-off value step by step | Still holds at 2 %, drops at 1 %. **Setting is 10 %** | ✅ |
| 3 | Flipper current profile | ESP32 Hall clamp on the 24 V mech rail, **test at 2 %** | ≈6 A inrush, then **≈0.1 A** held. An early ≈2 A reading was proven wrong by re-test | ✅ |
| 4a | Slow-blow vs stuck coil | 2 A SB, then 2.5 A SB | 2 A blew in under 0.5 s; 2.5 A didn't blow in 30 s | ✅ (informed choice) |
| 4b | RUEF250 | Stuck coil at ≈6.5 A | **Didn't trip within 15 s**, so rejected | ✅ |
| 4 | Stuck-coil protection | Coil held on, RUEF160 in circuit | RUEF160 trips in **under 10 s** | ✅ |
| 5 | PTC nuisance trips | Normal play | **No false trips** | ✅ |
| 7 | Diode polarity | After fuse-blow events | A reversed 1N4007 died and blew the 4 A port fuse; corrected polarity restored operation | ✅ |
| 8 | Chassis earth continuity | Meter from metal parts to the C14 earth | Failed until powder coat was scuffed; passes after | ✅ |
| 9 | ARGB sustained white | DOF `.ini` with permanent `ON White` triggers | Full white held (Configurator pulses too short for this) | ✅ |
| 10 | Toy and LED triggers | Dude's Cab Configurator manual triggers | All wired toys and LEDs respond | ✅ |
| 11 | End-to-end | VPX tables on a laptop over USB driving DOF | Toys and lighting work in play | ✅ |
| 13 | 24 V rail current with bumpers firing | ESP32 clamp on the 24 V rail, 20 ms sampling | Smoothed 5.5-7.2 A; **spikes 15-30 A** (≈5.7 A inrush per bumper plus documented switching spikes) | ✅ |
| 14 | Undercab strip direction | Arrangement changed; real DOF effects | Chases front to back with the playfield strips | ✅ |
| 12 | Rail monitor baseline | Idle cabinet, clamp zeroed | ≈0 ± 0.5 A, with brief spikes to ±1.5 A (noise) | ✅ |

## Pending tests
- Shunt + oscilloscope capture of a single coil firing (inrush vs switching spikes).
- Flipper sustained current at the configured **10 %**.
- Flipper **long hold** with the DS18B20 on the coil (temperature rise; PTC behaviour near its hold rating).
- Per-rail **peak and sustained** during a busy multiball table (completes the power budget).
- 24 V audio feeds once fused.
- Bumper LED flash circuit once fitted.
