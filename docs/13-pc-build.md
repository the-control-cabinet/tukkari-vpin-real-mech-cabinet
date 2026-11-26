# 13 · PC Build

[← Back to README](../README.md)

**Status: built, Nov 2026** ([video: I finally built the PC for my Tukkari Virtual Pinball cabinet!](https://www.youtube.com/watch?v=49bwwH7yKdk)). Replaces the laptop that proved the cabinet end to end. Commissioning (power-up, software, screens) is Part 2.

## Why this build
- A dedicated PC for the Tukkari widebody cab, driving **four screens**: a **4K 144 Hz OLED playfield** (main), the backglass, the DMD and the future topper, which is a **projector** (also the display for the internal gameplay camera, [08](08-gameplay-camera.md)).
- Headroom for the highest settings, plus **VR pinball on a Quest 3** within 2-3 years. That decided the GPU: the **RTX 5080** over the RTX 5070 Ti.
- The cab has plenty of room, and the motherboard sits **flat on a Tukkari plate**.

## Parts (£3,410.24)

| Part | Model | Price |
|---|---|---|
| GPU | Gigabyte RTX 5080 Gaming 16G | £1,575.00 |
| CPU | AMD Ryzen 7 9850X3D | £327.99 |
| Motherboard | Gigabyte X870 Aorus Elite WiFi7 | £239.98 |
| RAM | Corsair Vengeance 32 GB (2 × 16 GB) DDR5-6000 CL30 | £529.99 |
| SSD | Samsung 990 Pro 4 TB | £605.94 |
| PSU | Corsair RM850x | £104.99 |
| CPU cooler | Thermalright Peerless Assassin 120 SE ARGB | £26.35 |
| **Total** | | **£3,410.24** |

Not included: the Tukkari board, plates and STL prints, the 5 → 12 V step-up, cables.

## Build decisions and lessons

| Area | What was done | Lesson |
|---|---|---|
| Cooler airflow | Front-to-back along the cab. Tried a middle fan plus a rear fan, but the rear fan fouls the connector inlet, so back to plan A: **front + middle**, front fan clearing the RAM | Check clearances to the cab's connector inlet before choosing fan positions |
| Cooler standoffs | Only line up one way round | Orientation matters: dry-fit first |
| RAM and SSD | RAM in slots **A2/B2** (dual channel); SSD in the **primary M.2** slot | Follow the board manual's slot order |
| Cable tidy | Fan power and ARGB bundled together; PSU cables cable-tied in advance | Pre-dress cables before the board goes in |
| GPU bracket (Tukkari STL) | Sits off-centre; the ports were tight against it. Moved across and two holes re-drilled: ports clear, some ventilation partly covered | Worth a redesign for this card |
| Fixings for 3D prints | Wood screws were too thick; one head sheared off | Use **small machine screws and nuts**; redo properly |
| Assembly order | — | Fit the **cable cover piece before the motherboard** |
| Mounting | Board screws down with the supplied machine screws into Tukkari's pre-drilled holes; the second bumper row and the playfield hinge clear the PC | |

## Connections

| Header / port | Goes to |
|---|---|
| SYS_FAN headers | Cab inlet and exhaust fans |
| F_PANEL | Power LED and power button, wired to the **under-cab button** |
| Under-cab button LED | 12 V bulb on a **5 → 12 V step-up** (a 5 V bulb would also work), so it lights only when the board is powered |
| Rear USB | USB extensions and the sound card |
| Wi-Fi | External antenna fitted |
| USB-C | The **15" DMD**: one cable carries power and data, so the DMD isn't driven by the GPU (only some boards support this) |
| GPU | OLED playfield (DisplayPort → HDMI), backglass, future topper projector |

## Still open
- [ ] Proper machine screws and nuts for the 3D prints (replace the wood screws, including the sheared one).
- [ ] Decide which GPU port goes to which screen (playfield, backglass, topper projector), and how the projector is shared with the gameplay camera's Pi.
- [ ] Possible GPU bracket redesign for this card.
- [ ] Final wiring tidy-up.
- [ ] Part 2 video: commissioning (power-up, software, screens); move the frontend to PinUp Popper Baller.
