# 10 · Safety

[← Back to README](../README.md)

This cabinet combines **mains**, about **1.65 kW of DC supply capacity** (four Mean Well LRS supplies) and **inductive loads** that can overheat if left energised. These are the principles and how each is applied here. Verify everything before copying, because this is one specific build.

## 1. Mains (230 V AC)

| Principle | Applied here |
|---|---|
| A single, fused entry point | C14 inlet → distribution to PC, PSUs and amps ([220 V AC & PC diagram](../diagrams/220v-ac-and-pc-connections-v1.1.pdf)) |
| **Protective earth on all exposed metal** | Earth braid from the C14 inlet earth via the legs to the coin door. Lockdown bar and side rails bonded via the coin door |
| Powder coat is an insulator | Coating scuffed at every bolt and plate interface (or star washers used). Continuity was **not** achieved until this was done |
| Verify, don't assume | Continuity checked from every major metal part back to the C14 earth after assembly |
| Touch-safe terminals | PSU terminal covers fitted; mains and DC kept on separate sides with labels |
| Isolation for work | Unplug at the inlet, not just a switch. Allow PSU capacitors to discharge before touching terminals |

## 2. DC distribution and fusing

**Principle:** every conductor must be protected by a fuse no larger than the wire can safely carry. A PSU's own limp or current-limit mode isn't a substitute, because a 25-60 A supply can heat a thin wire long before it trips.

| Rail | PSU (max) | Inline fuse | Backhaul | What the fuse protects |
|---|---|---|---|---|
| 5 V | LRS-350-5 (60 A) | **30 A ANL** (was 60 A) | 3 × 10 AWG in, 12 AWG to a 25 A terminal block | The backhaul. Voltboard port fuses protect LED branches. ⚠️ **The leg from the 5 V terminal block to the direct Voltboard isn't separately fused** |
| 12 V | LRS-350-12 (29.2 A) | **20 A** | 12 AWG to a 25 A terminal block | The 12 AWG feed **and** the block, both correctly. Bunny port fuses protect each toy |
| 24 V mech | LRS-600-24 (25 A) | 30 A | 2 × 12 AWG to 25 A terminal block(s) | The backhaul. Bunny port fuses + PTCs protect each coil |
| 24 V audio | LRS-350-24 (14.6 A) | ⚠️ **None** | Three direct runs to the amps | **Gap**: see below |

> ⚠️ **5 V direct-Voltboard leg is unprotected.** A 30 A ANL can't protect a lighter wire downstream of the terminal block. **Recommended:** an inline fuse on that leg sized below the wire's rating (about 15 A for 14 AWG), or a heavier wire. This is on the roadmap.

> ⚠️ **24 V audio is unfused.** It was a deliberate shortcut (short single runs, no terminal block, fewer joints), but a chafed feed could carry the PSU's full output. **Recommended:** an inline fuse on each amp feed, close to the PSU, rated to the amp's draw and below the wire's capacity. This is on the roadmap.

> **Audio ground isolation (deliberate):** the audio PSU's negative isn't bonded to the common ground block. The amps reference to the sound card, which keeps coil return currents out of the audio ground.

## 3. Coil protection: layered by design

| Layer | Device | Protects against | Tested |
|---|---|---|---|
| 1 | Dude's Cab fall-off (**10 %**) + ≈60 s security delay | Normal heating; outputs left asserted | Hold still works at 2 % (test), drawing ≈0.1 A |
| 2 | **RUEF160 PTC** on all 10 playfield coils (knocker, chimes, shell bell: none yet) | A stuck coil (software, USB or exit fault) | **Trips in under 10 s; no false trips in play** |
| 3 | Bunny port slow-blow, **2.5 A on all coils** | Short circuits, wiring faults | 2 A blew in under 0.5 s (nuisance risk); 2.5 A didn't blow in 30 s on a stuck coil, which layer 2 covers |
| 4 | 1N4007 flyback diode across each coil | Inductive kick destroying Bunny outputs | Polarity matters: a reversed diode short-circuits the coil supply on firing, which killed the diode and blew the 4 A port fuse |

**Known trigger:** an abrupt VPX → PinUp Popper exit can leave outputs asserted. Layers 1 and 2 cover it.

## 4. Component polarity and ratings
- **Diodes:** band toward +24 V. Check before power-up; a reversed diode is a dead short when the coil fires.
- **Electrolytic capacitors** (gear motor filter, planned bumper-LED flash): observe polarity, and use a voltage rating comfortably above the rail (35 V on 24 V).
- **Wire gauge:** 18 AWG to toys; 10-14 AWG backhauls and Bunny ground returns, sized for concurrent peaks.

## 5. Thermal
- Coils and PTCs get hot by design. Keep wiring off coil bodies.
- PWM fall-off keeps a held flipper to a small current (≈0.1 A in the 2 % test), and the ≈60 s security delay limits hold duration. The RUEF160 covers the stuck-on case, where the full ≈6 A would otherwise flow.
- **Heat checks** after heavy play: the 25 A terminal blocks (especially 5 V under full white), fuses and PSU terminals.
- A DS18B20 is available for coil or enclosure temperature monitoring.

## 6. Disclaimer
One specific cabinet. All voltages, currents, fuse ratings and wiring are as measured or calculated here. **Incorrect coil or power wiring can damage parts or cause a fire.** No warranty.
