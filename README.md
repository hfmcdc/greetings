# Vaiga Sweets & Snacks — Deepavali Greeting

A digital greeting card for people who scan the QR code on the sweet box.
Static site. No build step, no framework, no backend.

```
index.html              the whole experience
audio/
  deepavali-music.mp3   starts only when the diya is tapped
```

## How the experience is structured

The page has two states, and the diya is the gate between them.

**Unlit** — reads top to bottom: "Happy Deepavali", then "Tap the diya to
begin", then a large lamp, then an explicit `Light the Diya` button. The
lamp's tap target is the full ~290px circle (padding, not just artwork),
with expanding rings, a resting glow and a small animated hand to signal
it. The lamp and the button call the same `light()` function.

The rest of the page exists in the DOM but the document is scroll-locked
(`html.sealed`) and hidden from screen readers, so there is nothing to
scroll past and nothing to skim ahead to.

**Lit** — the tap triggers, in one moment: flame ignition, a soft chime,
the music, and a ~4.6s celebration: firecrackers pop across the screen
(canvas fireworks with synthesised crackle sounds) while the whole screen
washes through vivid colours (violet, magenta, blue, teal, orange). The
colours then melt away into the warm burgundy/amber card, the greeting is
already showing, the page unlocks, and a clear "Scroll down to read your
wishes" button with animated arrows appears (tap it or just scroll).

The card below is short: one wish + thank-you, one contact block, one share
button, footer. About two and a half screens in total.

## Audio behaviour

Nothing loads or plays on page load (`preload="none"`, no autoplay).
`audio.play()` is called from inside the tap handler, which is the gesture
mobile browsers require. Volume fades 0 → 0.42 over about 2 seconds.

If playback is blocked, the control still appears so the visitor can start
it themselves. If the file is missing entirely, the control never appears
at all — no dead button, no error shown.

## Swapping the music

Replace `audio/deepavali-music.mp3` with a file of the same name, or edit
the `<source src="...">` near the top of `<body>`. A soft santoor / flute /
light tabla instrumental suits the piece best; make sure you hold the
rights for commercial use.

## Already configured

- Address: Lekshmi Nivas, T D Nagar 1, Kollam
- Phone: 70125 25750 (tap to call)
- Instagram: @vaigasweetsandsnacka
- Google Maps: https://maps.app.goo.gl/fLZevv5v9UzZQucq6

## Deploy on Vercel

1. Push this folder to a GitHub repo.
2. Vercel → Add New Project → import the repo.
3. Framework preset: **Other**. No build command, no output directory.
4. Deploy, then point the QR code at the resulting URL.

## Notes

- Mobile-first; tested layout from 360px up. No horizontal scroll.
- `prefers-reduced-motion` skips the fireworks and colour flashing, drops
  motes, rays and flicker, and unseals the page immediately on tap.
- The lamp is a real `<button>` with an aria-label, so it works from the
  keyboard. Music control exposes `aria-pressed`.
- The warm palette is deliberately fixed — a system light-mode setting
  will not turn the card into a white page.

## WhatsApp / social link preview

`og-image.jpg` (1200x630) is the picture shown when the link is shared.
WhatsApp needs an absolute URL, so after deploying, replace every
`https://YOUR-SITE.vercel.app` in the `<head>` of `index.html` with the real
site address. WhatsApp caches previews, so test with a fresh link or add
`?v=2` to the end.
