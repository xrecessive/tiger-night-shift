# TRAVELING TIGER CENTER: NIGHT SHIFT

*Five nights at the truck stop. Raja is still awake.*

A first-person, FNAF-style horror game set at the **Traveling Tiger Center** — the same diner, garage, fuel canopy, and tiger pen as the daylight game, after everyone else has gone home. You run the overnight desk for five nights, 12 AM to 6 AM, watching six cameras and keeping the doors sealed.

Built with **Godot 4.7** and exported for the **web**, sized for a 16:9 embed on Blogger.

**Live:** https://xrecessive.github.io/tiger-night-shift/ — published from [`xrecessive/tiger-night-shift`](https://github.com/xrecessive/tiger-night-shift) via GitHub Pages. The Blogger snippet is in `blogger-embed-night.html`.

The daytime management game is a separate project: [`xrecessive/tiger-stop`](https://github.com/xrecessive/tiger-stop) · https://xrecessive.github.io/tiger-stop/

---

## Play

Open the project in Godot and press **F5**, or run:

```bash
godot --path .
```

Survive from **12 AM to 6 AM** (45 seconds per in-game hour) for five nights. Doors and lights run off the same power supply as the monitor. When power hits zero, the office goes dark and something is already in the doorway.

### Controls

| Input | Action |
| --- | --- |
| Click / tap | Buttons, night cards, camera map |
| `SPACE` / `TAB` | Open / close the camera monitor |
| `Q` or `A` | Left door |
| `E` or `D` | Right door |
| `Z` / `C` | Left / right door light |
| `1`–`6` | Select a camera |
| `F` | Feed Raja (CAM 04 only) |
| `ESC` / on-screen **MENU** | Back to night select |
| `M` | Mute |

Mouse or touch. Runs in the browser — no download.

---

## The night crew

| Who | Path | Counter |
| --- | --- | --- |
| **Raja** | Tiger Pen → Lot → Left Door | Feed him on **CAM 04** (4% power, 20 s cooldown). Hunger also makes him push sooner. |
| **Faviola** | Diner → Back Hall → Left Door | Watch the hall, seal the left door, and check the light. |
| **Arturo** | Garage → Back Hall → Right Door | Watch the hall, seal the right door, and check the light. |

Doors hold them back and send them home. Open doors do not. Lights are free to look through but time out after four seconds, and everything you leave on drains power faster.

| Night | On the lot |
| --- | --- |
| 1 | Raja |
| 2 | Raja, Faviola |
| 3 | Faviola, Arturo |
| 4 | Raja, Faviola, Arturo |
| 5 | All three, faster |

Raja sleeps in the pen on nights he isn't hunting.

### The cameras

| Cam | Room |
| --- | --- |
| 01 | Diner |
| 02 | Garage |
| 03 | Pumps |
| 04 | Tiger Pen |
| 05 | Lot & Entrance |
| 06 | Back Hall |

---

## Project layout

```
project.godot             engine config, 1280x720 canvas
scenes/Main.tscn          single root Control
scripts/Night.gd          simulation: clock, power, doors, lights, threats, feed, win/lose
scripts/Main.gd           shell: flow, input, save file, web state hook
scripts/Room.gd           office, six camera feeds, blackout, menu backdrop
scripts/Hud.gd            top bar, command deck, monitor chrome, menus, jumpscares
scripts/ViewBase.gd       shared draw helpers and character art
scripts/UILayout.gd       screen rectangles and hit regions
scripts/Audio.gd          22 synthesized sound effects (no audio assets)
fonts/BebasNeue-Regular.ttf  display font (OFL, license in fonts/OFL.txt)
tests/night_test.gd       headless simulation checks
tests/ui_test.gd          full-scene flow checks
tests/shot.gd             Xvfb screenshot harness
export_presets.cfg        Web + Android presets (threads disabled)
blogger-embed-night.html  copy-paste iframe for Blogger
build/web/                exported playable build
```

All art is drawn procedurally with `CanvasItem` primitives, and every sound is synthesized at boot. There are no sprite or audio assets to import.

Unlocks are saved in `user://night_shift.cfg` (nights 1–5 plus cleared nights).

---

## Build

```bash
# web
godot --headless --export-release "Web" build/web/index.html

# android
tools/export_android.sh
```

`tools/package_web.sh` builds and zips the web export; `tools/deploy_web.sh` publishes it to GitHub Pages.

---

## Tests

```bash
godot --headless --path . -s tests/night_test.gd
xvfb-run -a -s "-screen 0 1280x720x24" godot --path . --rendering-driver opengl3 tests/ui_test.tscn
xvfb-run -a -s "-screen 0 1280x720x24" godot --path . --rendering-driver opengl3 tests/shot.tscn
```

---

## Credits

Starring the Traveling Tiger Center crew: Arturo, Faviola, Esther, Leti, Mireya, Ismael, Tony, Ashley, Adrianna, Raquel, Mark, Jacquelyn, Raul, Delada, Aurtorito, Roger, Letty.

**and RAJA as himself.**

Fake horror, no gore. Made for the night shift.
