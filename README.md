# Top Story

The daily Top Story: one animated news explainer a day, made by the "Daily Top Story" scheduled task.

- `latest.html` is always the newest story. Big Boi OS (the living-room TV's home screen) downloads it from
  `https://raw.githubusercontent.com/keithmancuso/top-story/main/latest.html` every few hours and plays it on a loop.
- `stories/<YYYY-MM-DD>-<slug>.html` keeps every day's story. The TV lists this folder (GitHub contents API) so
  Keith can flip back through past stories with Up/Down. Keep the date-first names: the TV sorts by them.
  The archive starts on 2026-10-24; the earlier stories used other stage sizes or no `__story` hook.

## Contract for each story

Each file is one self-contained HTML page (inline CSS and JS; web fonts from Google Fonts are fine) with:

- a fixed 432x768 portrait stage, scaled to fit the window,
- all readable content inside the safe box x 26-380, y 108-600 (stage px),
- `window.__story = { duration, seek(t) }`, where `seek(t)` renders frame `t` seconds in and stops the page's
  own playback.

The TV crops to y 96-616, drives the timeline with `seek()` to loop it, hides any Replay button, and makes
links inert. A file over 3 MB or without `__story` is ignored, and the TV keeps showing the last good story.
