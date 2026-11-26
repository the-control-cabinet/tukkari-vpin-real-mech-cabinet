# 11 · Videos: The Control Cabinet

[← Back to README](../README.md)

Channel: **[The Control Cabinet on YouTube](https://www.youtube.com/channel/UC5Cupmz7vlfcodpCX7k8iuQ)**, adventures in virtual pinball and Home Assistant.

| Video | Link | Topics folded into these docs |
|---|---|---|
| **I finally built the PC for my Tukkari Virtual Pinball cabinet!** (26 Nov 2026) | [watch](https://www.youtube.com/watch?v=49bwwH7yKdk) | The dedicated cab PC: RTX 5080 + 9850X3D (per the thumbnail); BOM and build notes in [13 · PC build](13-pc-build.md) |
| Virtual Pinball - Real-Mech Pop Bumper Assembly Guide, **Part 2** (15 Nov 2026, 24:35) | [watch](https://www.youtube.com/watch?v=C6_70nraSic) | LED bulbs in the pop bumpers flashing in sync with the coil strike; why the bumper's orientation matters ([04](04-mech-toys-and-coil-protection.md)) |
| I installed an HD LED Matrix into my Tukkari Virtual Pinball cab, **Parts 1-3** (Part 2 21 Oct, 22:00; Part 3 30 Oct, 10:20) | [Part 1](https://www.youtube.com/watch?v=-o0FjaZnpGI) · [Part 2](https://www.youtube.com/watch?v=0CcJNl-t4T8) · [Part 3](https://www.youtube.com/watch?v=h9ek9EePRaY) | Part 2: the mount in situ, wiring, Dude's Cab Configurator settings and first tests. Part 3: the DOF config, the matrix running in situ with custom GIFs, and how effective it is ([03](03-lighting-and-hd-matrix.md)) |
| Mortal Coils! How I protect the Real-Mech Coils | [watch](https://www.youtube.com/watch?v=ZbsF-g5vIfU) | RUEF160 PTCs; 35 ms / 0 % fall-off on bumpers, 10 % on flippers; why a 2.5 A slow-blow doesn't protect against a 6-7 A stuck coil; software + PTC layers |
| How I protect my Real Mech Flipper coils using hardware | [watch](https://www.youtube.com/watch?v=URfTXkrg76k) | Flipper-specific hardware protection |
| Why I installed in-line DC fuses | [watch](https://www.youtube.com/watch?v=xdAt1k0HEi0) | Inline fuses on 5 V (60 A, later reduced to **30 A**), 12 V and 24 V mech; none on 24 V audio; PSU limp-mode limitations. **Addendum:** fuse each branch for its thinnest wire ([01](01-architecture-power-and-grounding.md#branch-fusing-when-the-wire-gets-thinner)) |
| How I configured my Dudescab Bunny boards for Real Mech | [watch](https://www.youtube.com/watch?v=xSo2La5fzV8) | Bunny 1 and 2 port maps, fall-off delays and values, security delays, night mode, gear motor at 70 % |
| I'm going through Arnoz MX Buttons… | [watch](https://www.youtube.com/watch?v=NzLpOJl-FJ4) | MX button failures traced to a loose playfield-strip connection |
| Tour the guts of my Tukkari Virtual Pinball cab! | [Part 1](https://www.youtube.com/watch?v=klSNuN602sY) · [Part 2](https://www.youtube.com/watch?v=AOLksZjaci8) · [Part 3](https://www.youtube.com/watch?v=pzLITTsYfg4) | Physical layout, power, boards, cable management |
| Sneak peek of my custom Medieval Madness topper | [watch](https://www.youtube.com/watch?v=NNeiCwCUsZ4) | Topper |
| Virtual Pinball: Real-Mech Pop Bumper Assembly Guide (8 Nov 2026, 18:34; long version) | [watch](https://www.youtube.com/watch?v=rJyJR4AEaiQ) | Pop bumper assembly. **Corrections:** ignore the coil wiring shown (the 1N4007 diode wasn't fitted when filmed; final wiring in [04](04-mech-toys-and-coil-protection.md)); the fibre ("Bakelite") yoke is fitted on the **other side** of the metal yoke in this cabinet, so the return stroke lands on fibre rather than metal (no yoke-operated scoring switch here; factory order and reasoning in [04](04-mech-toys-and-coil-protection.md#fibre-yoke-orientation-why-this-cabinet-differs-from-the-factory)) |
| Tukkari Real-Mech add-on install (Parts 5 and 6) | [Part 5](https://www.youtube.com/watch?v=k3RY8v4qDzQ) | Real-mech installation |

## Shorts

| Short | Link | Topic |
|---|---|---|
| Coming Soon Preview Short | [watch](https://www.youtube.com/shorts/IUJwHqt_WBU) | What's coming to the channel |
| Pop Bumper Assembly Correction! | [watch](https://www.youtube.com/shorts/0rA8RSkf7PE) | The fibre yoke position correction to the pop bumper guide ([04](04-mech-toys-and-coil-protection.md#fibre-yoke-orientation-why-this-cabinet-differs-from-the-factory)) |
| Install LEDs in your Pinball Pop Bumpers! | [watch](https://www.youtube.com/shorts/WHq9BmF19uA) | The bumper flash bulbs (full version: Pop Bumper Part 2) |
| Virtual Pinball Real Mech Assembly | [watch](https://www.youtube.com/shorts/efrVuufDd_M) | Short version of the pop bumper assembly guide |
| Medieval Madness Custom Topper | [watch](https://www.youtube.com/shorts/UcTnN8SDz70) | The custom topper |
| Medieval Madness Custom Pin Gulp! | [watch](https://www.youtube.com/shorts/XHSpaCP9QCE) | A 3D-printed Medieval Madness castle (credit: soulrider911 on MakerWorld) |

Earlier shorts also cover thermistors (RUEF160), modified MX button leaf mounts and 3D-printed coin-leaf mounts.

**Coming next:** why I installed a 2nd gear motor; doubling up on SSF ("Double Bass"); a new and improved HD matrix mount for the Tukkari cabinet. **Later:** installing the custom Medieval Madness topper, optimising nudging with DudesCab, setting up the cab software, and monitoring the cab in Home Assistant with current clamps. Also planned: the internal gameplay camera.

**Corrections policy.** Published videos aren't re-uploaded to fix mistakes (that resets their stats); corrections go in cards, pinned comments, these docs, or a follow-up video. Known: the pop bumper guide's coil wiring and fibre yoke position (above); the in-line fuses video's branch-fusing addendum (above).

Related, in other repos: the three-part **mains water flow meter and pressure gauge** series (Oct 2026) is in the water monitoring project.
