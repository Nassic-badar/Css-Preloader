# Nexus Preloader

A futuristic, pure-CSS loading overlay: counter-rotating HUD rings, a radar sweep,
an orbiting particle, a pulsing core and a scanning progress bar.

**Zero page chrome.** No background colour, no wrapper page — the overlay is fully
transparent, so your website stays visible behind it and the loader appears dead
centre of the viewport.

## Files

| File | What it is |
| --- | --- |
| `loader.css` | The loader only. No `body`, `html` or global rules — safe to drop into any project. |
| `index.html` | A demo page with a fake website behind the loader, plus a backdrop switcher. |

## Use it on your site

1. Add the stylesheet:

```html
<link rel="stylesheet" href="loader.css">
```

2. Paste the overlay markup anywhere inside `<body>`:

```html
<div class="preloader" role="status" aria-live="polite" aria-label="Loading">
  <div class="pl-scene">
    <span class="pl-halo" aria-hidden="true"></span>
    <span class="pl-sweep" aria-hidden="true"></span>
    <span class="pl-ticks" aria-hidden="true"></span>
    <span class="pl-arc pl-arc--a" aria-hidden="true"></span>
    <span class="pl-arc pl-arc--b" aria-hidden="true"></span>
    <span class="pl-arc pl-arc--c" aria-hidden="true"></span>
    <span class="pl-orbit" aria-hidden="true"></span>
    <span class="pl-core" aria-hidden="true"><span></span></span>
  </div>

  <div class="pl-label">
    <span>Loading</span>
    <span aria-hidden="true"><i>.</i><i>.</i><i>.</i></span>
  </div>

  <div class="pl-bar" aria-hidden="true"><span></span></div>
</div>
```

3. Hide it when your content is ready — it fades out smoothly:

```js
window.addEventListener("load", () => {
  const preloader = document.querySelector(".preloader");
  preloader.classList.add("is-done");          // fade out
  setTimeout(() => preloader.remove(), 500);    // optional: remove from DOM
});
```

## Why it never fights your site

* `position: fixed; inset: 0` with `background: transparent` — only the loader paints.
* `pointer-events: none` — clicks, hovers and scrolling still reach the page underneath.
* All selectors are namespaced under `.preloader` / `.pl-*`, so no global resets leak.
* Sizing comes from one variable, so it scales with the viewport:

```css
.preloader {
  --pl-accent: #22d3ee;   /* primary neon colour */
  --pl-accent-2: #818cf8; /* secondary ring colour */
  --pl-size: clamp(190px, 46vmin, 250px);
}
```

## Embed inside one section instead of the whole page

Make the container the positioning context and switch the overlay to
`position: absolute`:

```css
.my-panel { position: relative; }
.my-panel .preloader { position: absolute; }
```
