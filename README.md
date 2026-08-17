# Ultra-Enhancer — Video Color Grader

A Manifest V3 Chrome/Brave extension that color-grades web video live using CSS
and SVG filters. Works on any site with an HTML5 `<video>` element.

## Load it

1. Go to `chrome://extensions` (or `brave://extensions`).
2. Enable **Developer mode** (top right).
3. **Load unpacked** → select this folder.
4. Open any page with a video, click the Ultra-Enhancer icon, drag the sliders.

After editing files: reload the extension card **and** reload the tab.

## How it works

- The content script runs on every site (respecting the "YouTube only" scope
  setting) and injects one `<style>` rule that filters the video. It targets the
  video's wrapper — on YouTube the `.html5-video-container`, elsewhere the
  parent via `:has(> video)` — so grading survives Chrome's hardware overlay.
- Basic adjustments are cheap CSS filter functions. Tone (shadows/midtones/
  highlights), denoise, clarity, sharpness and bloom use an injected SVG filter,
  referenced from the CSS filter list via `url(#...)` — added only when in use.
- Storage: `{ enabled, active, scope, theme, profiles: [12] }`. The popup edits
  the active profile and every change auto-saves; the content script reacts via
  `chrome.storage.onChanged`.

## Features

- 12 profiles, one tap to switch, auto-saved per device.
- 14 one-tap Ready Modes (content type, lighting, looks, resolution enhancers).
- Full Light / Color / Detail controls, including a tone curve and detail passes.
- Light and dark popup themes.
- Runs on all sites or YouTube only.

## What's next

- Warm↔Cool temperature (`feColorMatrix`) in the SVG pipeline.
- Renamable profiles; export/import; optional cross-device sync.
