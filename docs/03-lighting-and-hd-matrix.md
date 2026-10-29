# 03 · Lighting and the HD Matrix

[← Back to README](../README.md)

---

## CSD HD Matrix — Physical, Power, and Configuration

Six Cleveland Software Design 256-LED panels (1536 LEDs total) mounted in a line at the top of the playfield / base of the backbox.

![HD matrix underside wiring](../images/hd-matrix-underside-wiring.webp)
*Underside of the finished matrix mount showing power injection and data chaining across the six panels.*

### Panel connectors and orientation
Each panel has three rear connectors along one edge:  
- 3-pin: power + data in  
- 2-pin: power only  
- 3-pin: power + data out  

Panels installed with connectors along the bottom edge when viewed from the player side (LEDs facing the player). This orientation was chosen so the connector pigtails point upward toward the exit holes at the top edge of the mount and disappear into the cabinet.

### Data snake (confirmed against CSD documentation)
With connectors at the bottom (player view): data enters at bottom-left, travels up the first column, steps right, travels down the next column, steps right, travels up, and so on, exiting at bottom-right.  
This matches the physical “in” connector location. Alternative 180° rotation per panel was evaluated and rejected because it would force wires to exit downward.

### Data distribution
Three Donny ports, each feeding a pair of panels:  
- Donny port 6 → leftmost panel → second panel  
- Donny port 7 → third panel → fourth panel  
- Donny port 8 → fifth panel → rightmost panel  

Paired chaining preserves frame rate. Using six individual Donny ports was considered and rejected as unnecessary.  
In the Dude’s Cab Configurator the matrix is defined as 96 wide × 16 high on port 6; the two splits are automatically assigned to ports 7 and 8.

### Power injection
Every panel receives a power injection.  
Two Voltboard channels (each protected by a 10 A slow-blow) feed the matrix area via a quick-connector rated ~7 A per contact. From that point the feed is split locally to the six panels.  
Existing 3-pin cables were used for both data and parallel power injection because 2-pin power-only cables were not on hand. Injecting on the “in” 3-pin versus the middle 2-pin makes no meaningful difference provided the injection is local to the panel.

Full power topology: [DC Power Supply diagram](../diagrams/dc-power-supply-v1.6.pdf).
Theoretical maximum ≈ 18 A if all 1536 LEDs are driven at full white. In practice the matrix shows logos and flashing patterns; a solid full-white block does not occur during gameplay. The two 10 A Voltboard channels plus local splitting were judged sufficient.

### Reference ground
A reference ground conductor is run alongside long Donny data lines and connected to 5 V ground at the matrix end only. It is left unconnected (or carefully managed) at the Donny end to avoid ground loops while still providing a local return reference that reduces interference.

### Test notes
Dude’s Cab Configurator test modes (RGB, Colours, Laser) produce only short pulses. Sustained 100 % white for current-draw or visual verification required direct edits to directoutputconfig30.ini using permanent ON White triggers with appropriate area parameters.

---

## Lighting and LEDs

### ARGB loads (5 V)
- CSD matrix: 6 × 256 = 1536 LEDs
- Playfield edge strips + undercab strips: ~134 LEDs each
- Speaker rings: 2 × 128 LEDs, chained on one Donny port, wired **inner → outer** (effects grow from the centre outwards, which is kept as a feature)
- Arnoz MX flashers: **19 × 4 LEDs** (5 commissioned; 14 for a custom topper in progress)
- Arnoz MX buttons: 5 units
- ARGB fans: 3 units
- Approximate total ARGB LEDs: ~2370+

### Current estimates (full white)
- Typical WS2812-style: 50–60 mA per LED at 100 % white.
- CSD panels: ~3 A max per panel.
- Practical gameplay: far lower (logos, flashing, partial illumination). 100 % solid white across everything is a test condition only.

### 12 V lighting
- Interior strip (coin-door interlock controlled).
- Some button LEDs.
- Planned pop-bumper LEDs (paralleled at coil with resistor + optional cap).

### Power injection
- Power is **star** from the Voltboards (order doesn't matter); data is **series**.
- 1 m 144-LED strips: one-end injection is fine at normal brightness, but full white shows a cut-off from voltage drop, so inject at **both ends** for full-white reliability.
- Inject power every few hundred LEDs on long strips.
- Matrix: inject at every panel (using available 3-pin connectors in parallel with data where needed).
- Voltboard fuses protect individual branches.

### Tint / covers
- The **LED strip itself is smoked-tint**; the aluminium channel covers are **clear**. Tint film on the covers was impractical.
- Backglass: spray-painted black (Plasti-Kote) on rear side after tape-masking; second coat applied after wind-related issues on first attempt.

---

## Configuration rules learned

| Rule | Detail |
|---|---|
| Chain order on the button channels | Flipper → magna (→ fire) → side strip → undercab strip. Strips last, so only one front data wire is needed |
| LED counts must match reality | A segment defined short by *n* LEDs makes only its last *n* LEDs show the next segment's effect, a localised bleed. Count with the Configurator test patterns |
| Strip direction | Undercab strips are fed from the rear; **Arrangement** reverses them so they chase front to back with the side strips. The Laser test always shows the physical direction, by design |
| Cut strips | Sometimes need a higher LED count in the Configurator to light fully |
| ARGB fans | 12 V motor + 5 V ARGB. Connector pin order varies, so check with a meter first |
| Apply changes | **Send Config → Save to Memory**, then regenerate the DOF config |
| `cabinet.xml` | Not used with an MX Donny |

