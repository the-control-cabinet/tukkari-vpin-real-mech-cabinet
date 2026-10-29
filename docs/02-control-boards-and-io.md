# 02 · Control Boards and I/O Allocation

[← Back to README](../README.md) · Points list: [`data/points-list.csv`](../data/points-list.csv)

## Board overview

| Board | Qty | Role |
|---|---|---|
| Dude's Cab V1 | 1 | Main controller over USB; drives everything below |
| **Bunny** | **2** | 16 PWM low-side MOSFET outputs each (8 A per output, 40 A per board), opto-isolated, 12 V logic supply |
| MX Donny | 1 | 8 ARGB data outputs (up to about 512 LEDs each); data only |
| Voltboard V4 | 3 | Fused 5 V distribution (4 outputs each) |
| The Brain V1.2 | 1 | Undercab buttons and the coin door interlock |
| Button Board | 4 | Cabinet button inputs |
| Potar | 1 | Plunger |

**Principle:** every toy's positive is always live from its rail; the Bunny switches the **negative**. Data and power are separate: the Donny sends data, the Voltboards supply power.

---

## Bunny 1: outputs

| Port | Device | Rail | Port fuse | PTC | Suppression |
|---|---|---|---|---|---|
| 1 | Flipper left (FL-11629 power winding) | 24 V | 2.5 A SB | RUEF160 | 1N4007 |
| 2 | Sling left | 24 V | 2.5 A SB | RUEF160 | 1N4007 |
| 3 | Flipper right (FL-11629 power winding) | 24 V | 2.5 A SB | RUEF160 | 1N4007 |
| 4 | Sling right | 24 V | 2.5 A SB | RUEF160 | 1N4007 |
| 5 | Bumper middle left (AE-23-800) | 24 V | 2.5 A SB | RUEF160 | 1N4007 |
| 6 | Bumper middle centre (AE-23-800) | 24 V | 2.5 A SB | RUEF160 | 1N4007 |
| 7 | Bumper middle right (AE-23-800) | 24 V | 2.5 A SB | RUEF160 | 1N4007 |
| 8 | Knocker (Data East/Sega) | 24 V | 2.5 A SB | none yet | 1N4007 |
| 9 | Shaker (Stern Spike kit, PinSound) | 12 V → 7 V buck | | | La Nettoyeuse |
| 10 | Coin right LED | 12 V | | | |
| 11 | Repeating (fire-alarm) bell | 12 V | | | La Nettoyeuse |
| 12 | Beacons (pair) | 12 V | | | none needed |
| 13 | Topper blower (12 V truck fan) | 12 V | | | La Nettoyeuse |
| 14 | Coin left LED | 12 V | | | |
| 15 | DTG strobes | 12 V | | | |
| 16 | Start button LED | 12 V | | | |

## Bunny 2: outputs

| Port | Device | Rail | Port fuse | PTC | Suppression |
|---|---|---|---|---|---|
| 1 | Shell bell small (3") | 24 V | 2.5 A SB | none yet | 1N4007 |
| 2 | Chime small | 24 V | 2.5 A SB | none yet | 1N4007 |
| 3 | Chime medium | 24 V | 2.5 A SB | none yet | 1N4007 |
| 4 | Chime large | 24 V | 2.5 A SB | none yet | 1N4007 |
| 5 | Shell bell large (4") | 24 V | 2.5 A SB | none yet | 1N4007 |
| 6 | Bumper rear left (AE-23-800) | 24 V | 2.5 A SB | RUEF160 | 1N4007 |
| 7 | Bumper rear centre (AE-23-800) | 24 V | 2.5 A SB | RUEF160 | 1N4007 |
| 8 | Bumper rear right (AE-23-800) | 24 V | 2.5 A SB | RUEF160 | 1N4007 |
| 9 | Gear motor (VW) | 12 V | 5 A SB | | La Nettoyeuse |
| 10 | Gear motor 2 (planned) | 12 V | 5 A SB | | La Nettoyeuse |
| 11-16 | Spare | | | | |

- The flipper wiring is **+24 V on the right lug, Bunny on the middle lug, hold lug disconnected, diode band on the right lug** (see [04](04-mech-toys-and-coil-protection.md)).
- Port fuses not listed for the 12 V toys are as labelled on the board; they're to be added to the points list.
- RUEF160s on the knocker, chimes and shell bells are an outstanding decision.

![Bunny 2 port labels](../images/bunny-2-port-labels.jpg)
*Bunny 2 port labels. The photo shows the original 4 A SB coil fuses; all coil ports are now 2.5 A SB.*

![Gear motor on Bunny 2](../images/gear-motor-bunny2.webp)
*VW gear motor, driven from Bunny 2 port 9.*

### Bunny grounds
Each Bunny has two ground terminals for current sharing, returned with 14 AWG: one to the 24 V PSU and one to the 12 V PSU.

---

## MX Donny: ARGB data outputs

| Port | Load | Notes |
|---|---|---|
| 1 | Left flipper + left magna + fire button (MX) → left side strip → left undercab strip | Chain order: buttons first, strip last, so only one front data wire is needed |
| 2 | Right flipper + right magna (MX) → right side strip → right undercab strip | As left |
| 3 | Flashers (MX, 4 LEDs each) | 5 commissioned; 14 more for the custom topper |
| 4 | ARGB fans (3) | |
| 5 | Speaker rings (2 × 128 LEDs, chained) | Wired inner → outer, so effects grow from the centre outwards |
| **6, 7, 8** | **HD matrix**: 6 CSD panels as 3 pairs | Defined as 96 × 16 on port 6; splits land on 7 and 8 |

*The contents of ports 1-5 are confirmed. The exact order of 1-5 is to be verified against the Configurator.*

- **Undercab strips** are fed with data from the **rear**, so their order is reversed with **Arrangement** in the Configurator. They now chase front to back together with the side strips.
- **LED counts must match reality.** If a segment is defined shorter than it is, only that many LEDs at its tail take the *next* segment's effect, which is a localised bleed. Count with the Configurator's test patterns, then **Send Config → Save to Memory**.
- **No `cabinet.xml`** when using an MX Donny.

### Reference ground and Donny ground
- Data runs over about 1 m: twist the data with a dedicated reference ground, connected to the local 5 V ground **only at the far (LED) end**.
- The Donny's ground terminal goes to the 5 V ground.

---

## Voltboards: 5 V power

| Voltboard | Output 1 | Output 2 | Output 3 | Output 4 |
|---|---|---|---|---|
| Main cab 1 | Left flipper/magna + left side strip | Right flipper/magna + right side strip | Spare | Spare |
| Main cab 2 | Matrix (primary) | Matrix (secondary) | ARGB fans (3) | Spare |
| Backbox | Speaker rings | Topper flashers | Undercab left | Undercab right |

- **Power is star (parallel) from the Voltboards**, so order doesn't matter. **Data is series.**
- The matrix's two outputs (10 A slow-blow each) inject at every panel.
- 1 m 144-LED strips are fine powered from one end at normal brightness. Full white shows a cut-off, so inject at **both ends** for full-white reliability.

---

## Inputs

| Board | Inputs |
|---|---|
| Button Board 1 | Left flipper, left magna, start, return (+ spares) |
| Button Board 2 | Fire, extra ball, coin return / add coins (+ spares) |
| Button Board 3 | Right flipper, right magna, launch, coin slot |
| Button Board 4 | Tilt |
| The Brain | Undercab buttons (Quit, Vol+, Vol-, Menu); **coin door interlock on the DOOR terminal** |
| Potar | Plunger |

- **Coin door interlock (E79-30A, DPDT):** pole 1 goes to the Brain DOOR terminal; pole 2 switches the 12 V interior LED strips.
- **Leaf switches** (Williams/Bally SW-1A-194, small) have no polarity; star the grounds locally.
- **Tilt bob:** a lower bob position makes it less sensitive. Sensitivity can also be adjusted in software.
- **PC power button and undercab button LEDs** run from the motherboard PWR_LED (5 V) through an **LM2577 boost converter** to 12 V. They light whenever the PC is on, so they don't need a Bunny port.
