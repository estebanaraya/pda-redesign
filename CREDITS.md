# Credits: PDA Redesign 0.4.0-alpha

Public alpha for testing. Build of 2026-11-05. This is a G.A.M.M.A. addon: where something comes from another
mod it is credited "original author, from Stalker GAMMA". S.T.A.L.K.E.R. is a trademark of GSC Game World. This is an
unofficial, free, non-commercial fan addon.

What is in this package, and what is not:

- Code, interface textures, icons, shaders, sounds and text are written or generated for this project. The textures are
  built from glyph, shape and pixel definitions in the project, apart from the limb readout's body figure (below); the
  sounds are synthesised; the fonts are bitmap atlases rendered from the two fonts below.
- No art, texture, model, audio or shader file from another mod is bundled, except Wearable Devices' body silhouette, cut
  into the HUD's limb atlas (next section). Other mods are read,
  called or wrapped by name at run time, from the player's own install.
- The code derived from Wearable Devices is the CRT pattern in `pdar_crt.ps` and the stat rule `get_state` in `utils_pdar_state.script` (next section). The pixel shaders carry the scaffold of the
  Modded Exes' `hud_default`. The talk window's layout files keep the element names and rects of G.A.M.M.A. Enhanced GUI HUD's
  (The game and the pack, below).

## Wearable Devices

Sulik, Jeremussy and Wiarubane, Wearable Devices (https://github.com/sulikz/st-wearable-devices). All rights reserved by
its authors. The addon requires Wearable Devices 0.9.2 or later and is not tested against any older version.

**Permission.** On 2026-10-16 the Wearable Devices team agreed to reuse of their art and the `wdcrt` shader in this
addon, bundled, with credit. On 2026-10-27 the Wearable Devices team widened that permission: in Esteban's words, to "bring in anything or reuse anything from there in this setup". Both agreements were given in conversation and relayed by Esteban; there is no written copy in
the project. Under the 2026-10-27 permission the CRT pass's shader `pdar_crt.ps` carries Wearable Devices' `crt_pattern`
(derived code, bundled, credited) and includes Wearable Devices' `wd_crt_promin_panel.h` (its CRT constants) from the
installed Wearable Devices when it compiles. This build bundles one piece of Wearable Devices art, the body silhouette (below), and not the `wdcrt` shader. The
Promin and Vektor icons and the map arrow atlas are read at run time from the installed Wearable Devices.
The PDA map draws Wearable Devices' map icons by their texture ids at run
time (`wd_nav_icons`), follows its greyscale map shading (plain luma) in the `pdar_gray` look, and carries the PROMIN's five
colour values (SERVICE, FIRE, EXIT, text, tracked) in `utils_pdar_map_icons_table.script`.

**Design.** The look extends the Wearable Devices Promin language, on the PDA. Promin colour values informed the colour
tokens (cited in `pda/tokens`, not part of this package). The 2026-10-16 agreement covers the art and the shader; the colour values
and the design language are not named in it.

**Code derived from Wearable Devices:** two files.

- `pdar_crt.ps`: the function `crt_pattern` and the four fade constants it reads, copied unchanged from Wearable Devices 0.9.2
  `wd_crt.h` (lines 12 to 31 and 6 to 9), under the 2026-10-27 permission; a comment above it names the source.
- `utils_pdar_state.script`: the function `get_state` (a stat to ok, warn or crit) and its thresholds `WARN_AT` 0.5 and
  `CRIT_AT` 0.25, the same name, signature, thresholds and comparison as Wearable Devices 0.9.0 `wd_face_tones.script` `get_state`
  (lines 12 to 21), with a guard added for a missing value and a clamp to 0 to 1; under the 2026-10-27 permission; the
  file's header names the source.

Two pieces used to follow the shape of Wearable Devices code (a DDS header reader and a texture size loop, in the texture map backend). They were removed on 2026-10-22 with that backend.

A third match is an interoperability constant, not copied logic: `utils_pdar_hud_hide.script` parks the game's ammo statics
at the same 4000-unit offset (`PARK_OFF`) Wearable Devices uses, so Wearable Devices sees its own park.

**Art and technique from Wearable Devices:**

- Body silhouette art: Wearable Devices by Sulik, Jeremussy & Wiarubane (PROMIN BIO page sprites)
- The fill technique after Wearable Devices' wd_silhouette.script

The AR HUD's limb readout draws Wearable Devices' body figure, under the 2026-10-27 permission. Its seven pieces
(`wd_bio_part_*` in Wearable Devices 0.9.0's `sprites.dds`) were cut by `scripts/cut-wd-body.js` (not in this package),
scaled to the readout, with an inner ring and a diagonal hatch made from each, and ship inside the limb atlas
(`textures/ui/ui_pdar_promin_hudl_*`). Each limb fills as Wearable Devices fills its BIO page: the piece's own texture cut
from the bottom across the limb's painted span. That code is ours (`utils_pdar_kit_hud_crop.script`,
`utils_pdar_hud_limbs_fig.script`).

**Read at run time, nothing copied:** `wd_hud`, `wd_inspect`, `wd_compass`, `wd_slots`, `wd_attach`, `wd_map_*`,
`wd_level_transitions`, `d_promin`, `d_vektor` and `d_watch`, for navigation on the HUD map, the worn-device complement,
the inventory slots (Forearm, Wrist, Bracer, Patch, Side) and Home's device cells.

## Fonts

Both are rendered into bitmap atlases (`textures/ui/pdar_font_*`). The licence texts are in `licenses/`.

- **JetBrains Mono.** Copyright 2020 The JetBrains Mono Project Authors (https://github.com/JetBrains/JetBrainsMono).
  SIL Open Font License, Version 1.1. Text: `licenses/OFL-JetBrainsMono.txt`.
- **IBM Plex Sans.** Copyright 2017 IBM Corp., with Reserved Font Name "Plex" (https://github.com/IBM/plex). SIL Open Font
  License, Version 1.1. Text: `licenses/OFL-IBMPlexSans.txt`. The atlases are a converted form of the font and carry
  neutral `pdar_` names, as the Reserved Font Name requires.

## Modded Exes

demonized and the Modded Exes contributors. The mod requires the Modded Exes engine APIs (the map widget, `pda_dynamic_tabs`,
the map spot functions) and DLTX and DXML. Every pixel shader of this addon (`shaders/r3/pdar_*.ps`) and its definition
(`pdar_*.s`) uses the scaffold of the Modded Exes' `hud_default`: the include lines, the entry signature and the HDR10 output
block, which a custom HUD shader on these exes has to end with. The effect code between them is ours, except Wearable
Devices' `crt_pattern` in `pdar_crt.ps` (above). `pdar_crt.ps` keeps the include lines and the entry signature but has no
HDR10 block: its output is a blend factor for what is already drawn, not a colour. The files we read name
no author and no licence. No Modded Exes file is bundled. `shaders/r3/pdar_hdr10.h` carries a copy of the part of the Modded Exes'
`hdr10.h` our UI shaders use (the HDR10 parameters, the sRGB and colourspace helpers and `HDR10_ToDisplay_UI`, unchanged), under that
header's own guard: where the engine ships `hdr10.h` (the Modded Exes), its own copy is used; where it does not (engine builds that dropped
HDR10 output), ours lets the shaders compile with HDR10 off.

The thermal, silhouette, reticle, ambient, glare and wave passes use the shader bus of xray-monolith pull request 805
("Shader bus v8", TheLostInPlace; not merged into the Modded Exes as of this build): its headers `bus_mask.h`,
`bus_hud_mask.h` and `bus_reproject.h` are included from the installed exes, not bundled. Without that exe those passes
fall back (README, Requirements).

## The game and the pack

- **S.T.A.L.K.E.R. Anomaly.** The Anomaly team, on GSC Game World's engine and assets. The AR visor and headset items use
  game models in place, by path (`dev_flash_1`, `goggles`, `helm_respirator`); the map, item and portrait art is drawn from the
  player's installed textures.
- **G.A.M.M.A.** Grokitach and the G.A.M.M.A. team. Read, wrapped or parked by name: Minimalist HUD, UI, Body Health System,
  Actor Damage Balancer, Medications Balance, Arti Recipes Overhaul, Economy, Rare Stashes Balance, Accurate Defense Values,
  Guns Have No Condition.
- **Mods in G.A.M.M.A. that the mod builds on.** MCM (RavenAscendant) for the options pages; SortingPlus,
  `rax_icon_layers`, `rax_persistent_highlight` and Encyclopedia Messages Restored (RavenAscendant), wrapped over, not copied.
- **Talk window.** `configs/ui/talk.xml`, `talk_16.xml` and `talk_21.xml` keep the element names, types and rects of
  G.A.M.M.A. Enhanced GUI HUD's talk window (INC, strangerism), which they replace; the plate, fonts and colours are ours.

## Binoculars

The three binocular items (Esteban, 2026-11-05), the FOB-45, the Yastrub and the Fighter, are **S.T.A.L.K.E.R. 2: Heart of
Chornobyl**'s binoculars by **GSC Game World**: their names, what each one shows, and their models and textures. The mod bundles,
per item, `meshes/dynamics/devices/pdar_binoc/pdar_binoc_s2_<item>_hud.ogf`, its motions `pdar_binoc_s2_<item>_hud_animation.omf`
and `textures/item/pdar_binoc_s2_<item>.dds`. The meshes and textures are GSC Game World's, read from a copy of S.T.A.L.K.E.R. 2
with `scripts/s2x`, a small extractor on **CUE4Parse** (FabianFG and contributors, Apache-2.0), the library **FModel** (4sval and
contributors, GPL-3.0) is built on; the property layouts come from the community **Stalker 2.0.4 .usmap** (BigChenga, Nexus Mods
STALKER 2 mods/2356; file `Stalker2 Mappings Usmap 2356 2.0.4 2026-08-30T12-13Z`, `Stalker2-5.5.4-0+UE5-d7e7826d.usmap`).
Each is placed in Blender by `scripts/build-bino-lens.js` (the X-Ray Blender add-on by PavelBlend) on the skeleton of
**S.T.A.L.K.E.R. 2 - HoC - Binoculars Remodel** by Gryf, centred in the hands as his model is, its eyepieces on his rim line,
and given the motions of **Classic Binoculars Remodel** (SoulCrystal), every motion of its `binoculars_hud_animation.omf`,
written again for that skeleton. With Gryf's mod enabled the three share its inventory icon.

## Works with (called or read at run time; no code included)

| Mod | Author |
|---|---|
| 293 PDA Taskboard (MIT) | iTheon, README credits TheMrDemonized |
| 478 Custom iTheon's PDA Taskboard | lizzardman |
| 463 Tasks QoL Pack | Serious |
| Personal Adjustable Waypoint, New Extensible RF Sources | Catspaw |
| Milspec PDA, Fair Fast Travel, Interaction Dot Marks | author not recorded in the project's audit |
| Item UI Improvements, QoL Bundle, Crafting Info in Tooltips | Utjan |
| Dynamic Icons Indicators | HarukaSai |
| 3DSS for G.A.M.M.A. | Redotix99, Andtheherois, party50 |
| Hideout Furniture Expansion | Maid, HarukaSai |
| FDDA Redone, FDDA | lizzardman, Feel_Fried |
| Toxic Air Redux | Priler |
| Mags Reloaded Forked | AndTheHeroIs, Priler |
| Ammo Check Enhanced Rework | Priler |
| FART | Erandis |
| Enhanced GUI (the talk window's layout, above) | INC, Erandis, strangerism |
| Identification UI | CrookR |
| SquareDOV | RavenAscendant |
| Tweaki_Breeki's RF Receiver Tasks | Tweaki_Breeki |
| Indirect Parts Favoriter | G_FLAT |
| Binoculars Rework (G.A.M.M.A.) | G.A.M.M.A. team |
| S.T.A.L.K.E.R. 2 - HoC - Binoculars Remodel; Classic Binoculars Remodel (the binocular's model, motions and raise, from the player's list) | Gryf; SoulCrystal |
| Screen Space Shaders (the heat target of the thermal and silhouette views) | Ascii1457 |
| Reworked Devices (the binocular zoom steps) | Meowie |
| Boomsticks and Sharpsticks (night vision scopes) | Mich |
| AMP Armor Mag Pouches (preview, optional) | author not named in its files |
| Minimal SOTA+ Complete (chest rigs, optional) | author not named in its files |
| Better Beef's NVGs (on Beef's NVG) | IndieSunpraiser; theRealBeef |

Nothing from PDA Radio Extended (Starcry_) or Anomaly Radio Extended (DesmanMetzger) is included: the radio lists what the
engine reports and ships no track and no playlist.

## Provenance notes

- The line glyphs of the interface kit are defined as path strings in this project. A comparison against public icon sets
  found no verbatim copy of a non-trivial path, but the check is not finished and no icon library is named in the project.
- Terms for the run-time sources are taken from each mod's own folder or its page as read on 2026-10-17; most carry none
  locally, so this file credits and copies nothing.
