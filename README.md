<div align="center">

# NPC Studio — Minecraft Bedrock add-on

**Pose, dress and film NPCs and mobs like a real studio. Made for thumbnails and cinematics, on phone and PC.**

[Download on CurseForge](https://www.curseforge.com/projects/1650549) ·
[Pack Builder website](https://noxeelmc-art.github.io/npc-studio-skins/) ·
[YouTube](https://youtube.com/@NoxeelMC) ·
[Discord](https://discord.gg/UGSPAUBUvF)

Minecraft Bedrock 26.30+ · no experimental toggles · GPL-3.0

</div>

---

## What it does

- **Studio panel**: a dark panel docked on the left with six tabs (Display, Pose, Presets, World, Camera, Layers). Menus switch instantly, with sliders, steppers, slots and head grids.
- **Live Editor**: one screen that never reloads. Toggles, sliders and lists change the NPC the moment you touch them.
- **Pose Mode**: a red / green / blue gizmo on the body part you look at. Walk around while you pose. 45+ poses, 19 looping animations, undo, redo and mirror.
- **Posable mobs**: 29 Minecraft mobs with their own look, posed part by part like an NPC.
- **Wardrobe**: exact copies of your gear, Trim Studio, enchant glint, and Hold poses for any item (also items from other add-ons).
- **58 cloaks**, 20 custom skin slots, 7 cape slots and 10 3D model slots, filled with the free Pack Builder website.
- **Cameras**: pyramid cameras that show the real shot, Fly Cam, 30 cinematic shots, Thirds and Cross guides, Photo Mode, green screen, depth map.
- **Share presets** as text codes or preset pack files.

## Install (players)

Download the `.mcaddon` from CurseForge and open it. Turn on **NPC Studio** in a world's Behavior Packs (the resource pack comes with it). Use the **Director's Baton** from your hotbar.

## Build it yourself

You need **Python 3** with **Pillow** (`pip install pillow`).

```bash
python3 tools/build.py          # writes dist/NPC Studio V3.mcaddon from BP/ and RP/
```

`BP/` and `RP/` are ready to use: you can also copy them into Minecraft's `development_behavior_packs` and `development_resource_packs` folders and edit live.

Many files in `BP/` and `RP/` are generated. If you change a generator, run them in this order (each later one edits the output of the earlier ones):

| Step | Tool | Makes |
|---|---|---|
| 1 | `tools/make_models.py` | player, outline and cape models |
| 2 | `tools/make_gizmo.py` | the Pose Mode gizmo |
| 3 | `tools/make_custom.py` | custom skin / cape / model slots, capes, view boxes |
| 4 | `tools/make_mobs.py` | posable mobs (`--src <bedrock-samples>/resource_pack` re-reads Minecraft's models) |
| 5 | `tools/make_ui.py` | the Studio panel (`RP/ui/server_form.json`) and its textures |
| 6 | `tools/build.py` | the `.mcaddon` |

Other tools: `make_icons.py` / `make_assets.py` (icons and textures), `make_depth_pack.py` (the optional Depth Map pack), `skin-pack-builder.html` + `make_site.py` (the Pack Builder website).

## How it's put together

| Where | What |
|---|---|
| `BP/scripts/main.js` | events and tools; everything starts here |
| `BP/scripts/panel.js`, `core.js` | the Studio panel: menus are ActionForms tagged with invisible colour codes that `RP/ui/server_form.json` draws as the docked panel |
| `BP/scripts/liveform.js` | the Live Editor (CustomForm + Observables, no reload) |
| `BP/scripts/rig.js`, `poseEditor.js` | pose properties, undo, Pose Mode gizmo |
| `BP/scripts/skins.js`, `mobdata.js` | skins, custom models and posable mobs (`skin_index`) |
| `BP/scripts/camera.js`, `cinema.js`, `shots.js`, `studio.js` | cameras, Fly Cam, cinematic shots, Photo Mode, layers |
| `BP/scripts/wardrobe.js`, `itemstate.js` | gear, trims, Item State and Hold poses |
| `BP/scripts/share.js` | preset codes and preset packs |
| `BP/entities/npc_studio.json` | the NPC entity: 32 properties drive pose, skin, cape and flags |

## Contributing

Issues and pull requests are welcome. Please test on a phone if you change the panel: NPC Studio is touch first.

## License

The code is **GPL-3.0-or-later** (`LICENSE`). Changed versions must stay open source, keep the credit to NoxeelMC, and use their own name and logo. Minecraft's models, textures and capes are not covered by the GPL. See `NOTICE.md` for details and credits.

Made by **NoxeelMC**. Inspired by the NPC Studio mod for Minecraft Java Edition. Not affiliated with Mojang or Microsoft.
