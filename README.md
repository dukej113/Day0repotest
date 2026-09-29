# DAY ZERO

A first-person survival game that runs in one HTML file.

Maple Court, 7:42 on a Saturday morning. The sprinklers are still going and the
lawns still need mowing, but the neighbours are out on the street and they
aren't waving back. Find the car keys, get to the wagon, and be gone before the
street fills up.

**Play it:** open `index.html` in any browser with WebGL2. No build step, no
server, no network — double-clicking the file is enough.

## Controls

| | |
|---|---|
| `W` `A` `S` `D` | move |
| mouse | look (click to lock the cursor) |
| left click | attack / fire |
| `Shift` | sprint (drains stamina) |
| `Space` | jump |
| `E` | interact / pick up |
| `1` `2` `3` / `Q` | switch weapon |
| `R` | reload |
| `Esc` | pause |
| `M` | mute |

Headshots do triple damage with firearms, a little over double with the
crowbar. Gunfire is loud — every shot pulls the street toward you.

## What's in the box

Everything is generated in code at load time. There are no images, no audio
files, no model files, and no third-party libraries — the whole game is the one
`index.html`.

- **Renderer** — a hand-written WebGL2 forward renderer: a single scene shader
  with hemispheric ambient, a sun, and a 2048² PCF shadow map that follows the
  player; a procedural sky (gradient, drifting fbm clouds, sun disk, and a
  column of smoke somewhere across town); and instanced billboards for blood,
  smoke, sparks, water and ground decals.
- **The neighbourhood** — seeded generation builds twelve houses (siding,
  gables, shingle courses, shutters, porches, chimneys, garages), a street with
  kerbs and worn centre-line dashes, driveways, walkways, fences, hedges,
  trees, parked cars, and the usual suburban clutter: mailboxes, bins, a swing
  set, a paddling pool, a bike dropped in the road. The whole world bakes down
  to one mesh and one draw call.
- **The neighbours** — a skinned humanoid rig assembled from boxes, drawn in a
  single call per zombie with bone matrices. Four types (shambler, lurcher,
  runner, crawler) share one authored motion set with per-instance phase, lean,
  limp and head-tilt, plus flinch, lunge, collapse and rise-from-the-lawn poses.
  They see, hear gunfire, lose you, and keep drifting your way anyway.
- **Audio** — every sound is synthesized on the fly from oscillators and noise:
  gunshots (crack, body, tail), the crowbar's whoosh, wet impacts, formant-
  filtered groans, footsteps that change with the surface you're on, a
  heartbeat when you're nearly out, and an ambient bed of wind, birdsong that
  thins out as the street fills, distant gunfire, a dog, and a car alarm two
  streets over. Groans and shots are positioned in 3D.

## Notes

Runs comfortably at 60 fps — the whole game loop costs about 0.25 ms a frame
with two dozen zombies active, and the scene is around 40 draw calls.

---

# ROAD TRIP (proof of concept)

`road-trip.html` is a separate, mobile-first low-poly driving game built on
Three.js r128, which it loads from cdnjs. Everything else is inline in that one
file.

**Play it:** open `road-trip.html` in a mobile or desktop browser. It needs a
network connection the first time to fetch Three.js.

- **Controls:** swipe left/right, tap the ◀ ▶ buttons, or tap either half of the
  screen. Arrow keys / `A` `D` work on desktop.
- **HUD:** fuel %, fatigue %, miles and time of day. The trip is time-compressed:
  1 mile per second, and 5 in-game minutes per second, so a full day/night
  cycle takes about 5 minutes. You leave at 4:00 PM, so dusk comes quickly.
- **Fuel** drains steadily. Running dry ends the trip. Fuel cans on the road
  give +8%, and hitting slow traffic costs 10%.
- **Fatigue** builds faster at night. Above 70% your eyes start to blink shut,
  and at 100% you doze off, which also ends the trip.
- **Encounters:** every 50 miles a card offers 2–3 choices that change your
  stats. The first one is always the Buc-ee's stop (+40% fuel, −10 min, or
  push through). After that you get a random rest area, diner, hitchhiker,
  gas stop, overlook, detour or motel (the motel only shows up at night).
- **World:** endless scrolling road with flat-shaded terrain that runs through
  six biomes (plains, desert, autumn hills, prairie, pine forest, red rock).
  The roadside is filled from object pools (trees, cacti, rocks, signs,
  billboards, houses, barns, silos, water towers, gas stations, diners) and
  lined with power poles, with distant mountains behind. The sky is a stepped
  gradient with a sun, moon and stars, and at night the headlights, tail
  lights and building windows light up.
