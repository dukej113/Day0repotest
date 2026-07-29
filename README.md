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
