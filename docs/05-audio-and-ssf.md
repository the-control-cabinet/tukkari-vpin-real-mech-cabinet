# 05 · Audio and SSF

[← Back to README](../README.md)

---

## Audio and SSF — Final Mapping

### Amps
Three amplifiers (**1 × XY-S220H + 2 × XY-S100H**) fed from the dedicated 24 V audio PSU (three direct runs from its screw terminals; no terminal block needed):
1. Backbox speakers + cabinet woofer
2. Front SSF exciters
3. Rear SSF exciters

### SSF hardware
- 4 × Dayton DAEX32EP-4 exciters (front pair and rear pair)
- 1 × Dayton BST-1 bass shaker; a **second BST-1 is planned** on the spare channel of the XY-S100H that drives the rear SSF exciters
- Backbox: Rockford Fosgate R1525X2 pair + PPS4-6 woofer
- Speaker cables are kept away from Donny data and 24 V mech wiring, crossing at 90° where they must

### Sound-card mapping (standard 7.1 SSF)
| Sound-card output | Typical colour | Drives | Physical location |
|-------------------|----------------|--------|-------------------|
| Front | Green | Backbox L/R (ROM, music, callouts) + cabinet woofer | Head of cabinet / backbox |
| Surround / Side | Grey | Rear playfield exciters | Back of playfield, near backglass |
| Back / Rear | Black | Front playfield exciters | Near flippers / closest to player |
| Centre / Sub | Orange / Yellow | Normally unused | — |

This matches the common VPX / Pinscape / community standard.  
Windows and 7.1 naming assume the listener is in the middle of the speakers; in a pinball cabinet the player stands in front, so “rear of table” (upper playfield) goes to Surround and “front of table” (flippers) goes to Back. VPX has a “front is rear of cab” option that compensates for this.

### Verification
1. In Windows Sound → Configure, click each speaker and note which physical pair plays.  
2. In VPX, test flipper sounds (should come from front exciters) vs upper-playfield / bumper / ball-roll sounds (should come from rear exciters).  
3. If front and back of the table are swapped, interchange the Surround and Back cables. Leave Front on the backbox.

### Notes
- StarTech (or equivalent) USB 7.1 used and proven. Loose jack connections can mimic a quiet channel — reseat before blaming the card.  
- Centre/Sub left disconnected in the pure SSF setup.  
- Direct PSU-to-amp wiring: no terminal block (not needed with three runs from a dedicated PSU) and **no fuses yet** (on the roadmap).
- The audio PSU's negative is **not bonded** to the cabinet's common ground. The amps reference to the sound card's ground, which keeps coil return currents out of the audio path.
- Short 18 AWG pigtails (under 10 cm) at the amp terminals are fine.
- **VPX:** Flippers and Contactors are set to **DOF only**, so the real coils provide the mechanical sound while ball roll and everything else goes to the SSF exciters. In **Night Mode** the real mech is off, which currently leaves no flipper or bumper sound (fix on the roadmap).  
- Onboard motherboard 7.1 remains an option for a future full PC build.

See also: [Power distribution](01-architecture-power-and-grounding.md).
