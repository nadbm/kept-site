# Kept marketing website

One static page. No build step, no dependencies: open `index.html` in a
browser, or serve the folder (`python3 -m http.server` from here).

This folder is separate from the app. The app's "no network" rule in
`CLAUDE.md` does not apply here (the page loads its fonts from Google Fonts),
and `scripts/validate.sh` does not check it.

## Files

- `index.html` — the whole page: styles, markup and scripts in one file.
- `kept-logo.svg` — the logo (also the favicon). The same mark is inlined in
  the navigation bar.

## How `index.html` is organised

Top to bottom inside `<style>`:

1. **Tokens** on `:root` (light), then the dark set twice: once under
   `prefers-color-scheme: dark` and once under `:root[data-theme="dark"]`.
   Change colours and fonts here. Keep all three blocks in step.
   Palette is "Slate": paper `#F2F0EA`, slate `#2F3E46`, manila `#E9C46A`.
   Fonts: Playfair Display (headings), Plus Jakarta Sans (body).
2. **Page styles**: nav, hero, stage, sections, pricing, FAQ.
3. **App-screen styles**, every rule scoped under `.d-win`. These draw the app
   windows shown on the page. They are HTML mockups, not screenshots, and use
   their own tokens (Geist, blue accent) so they look like the app, not the site.

Markup, in order: nav · hero (`.stage` holds the animated `.story` and the
stitched border) · `#how` · `#try` (interactive demo) · `#tabs` · `#packets` ·
`#features` · `#privacy` (`.band`) · `#compare` · `#why` · `#pricing` ·
`#faq` · closing call to action · footer.

Each app window is a `.shot` wrapping a fixed 1280×800 `.d-win`. A script
scales it to fit; `data-crop` / `data-crop-sm` ("x,y,w,h") crop it, the second
on narrow screens.

Scripts at the end: window scaling, scroll reveals, the dark-mode switch
(remembers the choice in `localStorage` under `kept-theme`), the demo, and
the hero animation.

## The hero animation (`.story`)

Three panels: sample documents (`.st-paper`), a small app window (`.mw`) and
reminders (`.st-rem`). The last script plays one step at a time for each of
three documents: drop, read (scan line, then the name and date highlight),
file (tab rises, row appears), remind. `data-at` on `.story` says which panel
is lit; `data-step` says which caption is lit. Timings are the numbers in the
`then(ms, …)` calls. It pauses when off screen or in a background tab.
Without script, or with `prefers-reduced-motion`, the `.story:not(.js)` rules
show a still picture of the finished state.

The sample passport always expires 90 days after the day the page is viewed.
The demo script computes the date and writes it into the elements with ids
starting `st-`, and into the passport sample of the `#try` demo.

## Hosting

Served by GitHub Pages from the public repo `nadbm/kept-site`
(https://nadbm.github.io/kept-site/), which holds only this folder's files.
The app repo is private, and Pages is not available for it on the free plan.
To publish a change, copy this folder's files into a clone of `kept-site`
and push its `main` branch.

## Before launch

- **Replace the app mockups with real screenshots** once the app's UI is
  final, or keep the mockups and update them to match the shipped app.
- **Check every claim against the app**: "nothing leaves your Mac", "secure",
  the 14-day trial, US$39, macOS 14, the calendar lead times, and the FAQ.
- **The "Why this exists" note is signed "Nadim, maker of Kept".** The owner
  must confirm the wording.
- "Download" buttons link to `#pricing`; there is no real download link yet.
- The name "Kept" has not been checked for availability.

## Rules for changes

- Plain language, no marketing clichés. No paired slogans, no rhetorical
  questions, no checkmark feature lists.
- People, addresses and documents shown are fictional (the Bennett household).
- Must work at 400px wide with no horizontal scroll, in light and dark, and
  with `prefers-reduced-motion`.
