# Vaiga Sweets & Snacks — Deepavali QR Microsite

A one-page, mobile-first Deepavali greeting for people who scan the QR code
on the sweet box. Static site, no build step, no backend.

## Structure

```
index.html          the entire site (HTML/CSS/JS in one file)
audio/
  deepavali-music.mp3   background music, looped, muted by default
```

## Deploy on Vercel

1. Push this folder to a GitHub repo (commit `index.html` and `audio/` as-is).
2. In Vercel, "Add New Project" → import that repo.
3. Framework preset: **Other** (it's a static site — no build command,
   no output directory needed; Vercel will serve `index.html` at the root).
4. Deploy. The QR code should point at the resulting `https://your-project.vercel.app` URL
   (or a custom domain if you attach one).

## Already filled in

- Address: Lekshmi Nivas, T D Nagar 1, Kollam
- Phone: 70125 25750 (tap-to-call)
- Google Maps link
- Background music: `audio/deepavali-music.mp3`

## If you ever want to swap the music

Replace `audio/deepavali-music.mp3` with a new file of the same name (or
update the `<source src="...">` path in `index.html`, around the top of the
`<body>`). The music button hides itself automatically if the file is
missing or fails to load, so nothing breaks either way.
