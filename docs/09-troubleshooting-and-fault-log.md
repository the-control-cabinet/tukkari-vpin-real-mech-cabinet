# 09 · Troubleshooting and Fault Log

[← Back to README](../README.md)

---

## Troubleshooting

### No DOF toys firing
- Confirm Dude’s Cab Configurator can manually trigger the same ports.
- Check DOF files location (DirectOutput root vs Config subfolder).
- Verify table name / ROM mapping matches the DOF config profile.
- Ensure VPX is  the bitness that matches the registered DOF.
- Check for missing cabinet.xml (not always required for Donny-only).

### ARGB not lighting or wrong colour
- Verify Donny channel assignment and matrix geometry / splits.
- Confirm power injection and Voltboard fuses.
- Use forced-white lines in directoutputconfig30.ini for isolation.
- Check reference ground on long data runs.

### Coil fuse blows immediately
- Diode polarity reversed or diode shorted.
- Coil wired with positive and ground swapped relative to diode.
- Dead short on the port.

### Coil does not fire
- Bunny port not assigned or not enabled.
- Fuse open.
- PTC tripped (cool and reset).
- Wiring open on positive or ground.

### Flipper weak or no hold
- Confirm the PWM fall-off value (configured at 10 %; the power winding still holds down to 2 % and drops at 1 %).
- Confirm the wiring: +24 V on the **right** lug, Bunny on the **middle** lug, left lug disconnected, diode band on the +24 V lug.
- Verify lug identification by resistance measurement with diodes lifted.

### Ground continuity missing on cabinet metal
- Powder coating at bolt/plate interfaces. Scuff or use star washers.

### Smell (TCP / electrical) during play
- Inspect for overheating PTC, resistor, or wire. Test all toys individually in configurator. Check for partially shorted diode or coil.

---

## MX Donny / MX Button Issue — Closed

### Original symptom
Dude’s Cab Configurator Laser test on the Donny channel carrying MX buttons only lit the first two LEDs. Downstream LEDs and the connected playfield strip failed.

### Initial diagnosis (superseded)
A failed Donny data-output driver was the leading hypothesis, consistent with a prior PCB cut on an MX button board that could have shorted data.

### Final root cause (resolved)
The Donny port was not faulty. The MX button board had blown again because of a loose connection on the playfield LED strip that was daisy-chained on the same data line. The intermittent/short condition damaged the button board (only two of four LEDs lighting and breaking the chain).

### Resolution
Loose connection on the playfield LED strip identified and corrected. Replacement MX button board installed. Channel now functions normally. Other Donny ports were unaffected throughout.

Status: Closed.

---

## Fault and lessons log (additional)

### Undercab strips chasing back-to-front (resolved)
- **Symptom:** effects on the 128-LED undercab strips ran the opposite way to the playfield strips.
- **Cause:** the undercab strips are fed with data from the **rear**; the playfield strips from the **front**.
- **Fix:** **Arrangement** in the Dude's Cab Configurator's Addressable LEDs tab, then **Send Config → Save to Memory**. Both sets now chase front to back together. No rewiring needed.
- **Lesson:** the Configurator's **Laser** test always runs in the physical wiring direction (its documented purpose), so it **doesn't** reverse when Arrangement changes. Verify with real DOF effects instead.

### Flipper resistance readings misleading
- **Symptom:** ≈0 Ω between two lugs; the hold winding read about 132 Ω.
- **Cause:** measuring with the diodes still connected.
- **Fix:** lift the diodes and re-measure: L–M 122 Ω, M–R 4 Ω, L–R 126 Ω. Diode orientation and wire thickness also help identify lugs.

### Reversed diode
- A diode fitted the wrong way round is a dead short when the Bunny switches on. It destroyed the diode and blew the port fuse. Band toward +24 V, always.

### ARGB fan not lighting
- Fan ARGB connector pin order (5 V / data / GND) differed from the expected order. Check with a meter before connecting. The fans are 12 V motors with 5 V ARGB.

### Cut strip not fully lit
- After cutting a strip, the Configurator sometimes needs a **higher** LED count than the physical count to light every LED.

### Buck converter won't adjust
- Several LM2596 modules had sticky trim pots, needing 20+ turns anticlockwise before the output started to fall. 7 V was confirmed good for the shaker.

### Full-white cut-off on 144-LED strips
- Powered from one end, the far end dims or cuts off at full white because of voltage drop. Inject at both ends.

