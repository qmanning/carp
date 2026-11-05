# CARP

*Covert Aquatic Reconnaissance Platforms. Lethal. Listening. Wet.*

A one-file interactive site for a defense contractor that sells armored attack fish. It's No. 01 of *Unhinged & On-Brief*, a series where the over-the-top website finally matches the brief.

**Live:** https://qmanning.com/labs/carp

## Why it exists

You've seen the fish. A huge painted koi swims across the page & follows your mouse, somebody calls it a one-shot & it gets reposted again. The one that started it for me was [Marina Budarina](https://budarina-koi.runable.site)'s koi page, & it's genuinely lovely.

The copies that followed were gorgeous & said nothing about the business. So the series asks one question: what if the brief DID match the design? If a site is going to look like a defense-tech launch, the company had better be selling something dramatic.

The long read is [the Unhinged & On-Brief article](https://qmanning.com/writing/unhinged-and-on-brief-carp). The whole build is on the [Experiment page](https://qmanning.com/experiments/carp).

## Run it

```bash
git clone https://github.com/qmanning/carp
cd carp
python3 -m http.server 8000
# open http://localhost:8000
```

It won't run from `file://` (WebGL blocks the textures). If you change something & nothing happens, hard reload.

## What's inside

| Part | What it does |
|---|---|
| `index.html` | The whole site: HTML, CSS & a WebGL2 engine. No build step, no dependencies. |
| `assets/fish-1.png` to `fish-3.png` | KOI-class, SILURUS (the catfish) & the tuna, painted top-down |
| `assets/photos/` | 11 fake "archival" photos, each split into a background (`-bg.jpg`) & a cutout (`-fg.webp`) |
| `assets/og.jpg` | The share card |

## How it works

- **It isn't 3D.** Each fish is a flat painted PNG drawn as a textured strip that bends as it swims, so the whole body turns, not just the head.
- **No orbiting.** Each fish wanders (Reynolds-style steering): it picks a spot in its zone, swims there, glides for a beat, then picks another, & it steers around the copy.
- **One water shader over everything:** wobble, ripples, drifting caustic light & a hair of chromatic aberration. The giant CARP letters are frosted glass: whatever swims behind them comes through blurred.
- **Lasers are drawn in code**, not painted into the art, so they can sweep or lock onto each section's target.
- **The archive photos are plates.** Each one is a cutout (BiRefNet via rembg) over a background with the people painted out (LaMa via IOPaint), so the people sit on their own plane, with pencil-sketch lines drawn in behind them.
- **Eight scroll sections**, from Infiltrate to Request clearance. The yellow button under each section's copy moves you to the next.

## Make your own fish

This is the prompt that finally worked, word for word:

```text
Same armored fish as the reference, seen from directly overhead like a scientific specimen photo:
camera perpendicular to the spine, no perspective or foreshortening, head and tail at the same scale.
Body perfectly straight and centered vertically, head pointing up, tail fully fanned out flat, both
pectoral fins spread symmetrically. Keep the armor, skull face, red eyes and sensor pod, but no laser
beams leaving the body. Isolated on a solid pure #00FF00 green background: no water, no ripples, no
reflections, no shadow. Tall 1024 x 2048 frame, whole fish visible with margin.
```

Key out the green, save it as a PNG & swap it in for one of the `fish-*.png` files. It won't be a one-shot for you either: the first pass gets you a fish, making it feel expensive takes a lot of rounds.

## Limits

- **Desktop first.** Phones get a simpler layout & it's not tuned like the desktop one.
- **Needs WebGL2 & a decent GPU.** Older machines will chug; lower the pixel ratio cap in `resize()`.
- **Fonts load from Google.** Offline, the giant CARP falls back to a system font.
- **The history is fake.** Every "archival" photo is AI-generated. No fish were deployed at Normandy. Probably.

## Credits

Inspired by [Marina Budarina](https://budarina-koi.runable.site)'s koi. Go play with hers, too. If you make your own on-brief brand, tag me. Credit the original creators, poke fun at the genre, never the person.

## License

The code (`index.html`) is MIT. The art (everything in `assets/`: the fish, the photos & the share card) is [CC BY-NC 4.0](https://creativecommons.org/licenses/by-nc/4.0/): free for non-commercial use, with credit. See [LICENSE](LICENSE).

---

Made by [Q Manning](https://qmanning.com) · [Source on GitHub](https://github.com/qmanning/carp) · [See it live in the Labs](https://qmanning.com/labs/carp)
