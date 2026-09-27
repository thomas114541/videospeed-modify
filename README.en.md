# Video Speed Controller

[简体中文](README.md) | [English](README.en.md)

> **This repository is an unofficial Simplified Chinese fork of [igrigorik/videospeed][upstream-link]**, based on upstream v0.11.1.
> It is community-maintained and not affiliated with the original author. See below for the official upstream version.

## Install

**Upstream official version** (recommended for most users):

[![Chrome Web Store][chrome-web-store-version]][chrome-web-store-link] [![Chrome Web Store Users][chrome-web-store-users-badge]][chrome-web-store-link] [![Chrome Web Store Users][chrome-web-store-stars]][chrome-web-store-link]

**This fork** (Simplified Chinese localization plus the controller changes below): not published to the Chrome Web Store. Build it from source and load it manually.

```bash
npm ci
npm run build
```

Then open `chrome://extensions`, enable "Developer mode" → "Load unpacked" → select the `dist/` directory.

**Video Speed Controller** gives you fine-grained control over the playback speed of any HTML5 video or audio element on any website.

## The science of speed watching

**tl;dr** — Higher playback speeds mean better engagement and better retention.

The average adult reads at around [250-300 words per minute][wpm-study] (wpm). Speech averages around 150 wpm; slide decks tend to land near 100 wpm. Given the choice, most viewers [speed playback up to roughly 1.3-1.5x][ms-study] to close that gap. Accelerated viewing [holds attention longer][byu-study] — faster delivery drives higher engagement. With practice, many settle at 2x or higher and find that [going back to 1x feels wrong][mit-study].

[wpm-study]: http://www.paperbecause.com/PIOP/files/f7/f7bb6bc5-2c4a-466f-9ae7-b483a2c0dca4.pdf
[ms-study]: http://research.microsoft.com/en-us/um/redmond/groups/coet/compression/chi99/paper.pdf
[byu-study]: http://www.enounce.com/docs/BYUPaper020319.pdf
[mit-study]: http://alumni.media.mit.edu/~barons/html/avios92.html#beasleyalteredspeech

HTML5 media elements already expose a native playback-rate API, but most players hide it or artificially cap it. Speed control should be easy and frequent: we do not read at one fixed pace, so we should not watch at one fixed speed either.

## Features

- **Universal** — works on any site with HTML5 media: YouTube, Netflix,
  Coursera, podcasts, local files, and more.
- **Video and audio** — controls both `<video>` and `<audio>` elements.
- **Fine-grained speed control** — adjust between 0.07x and 16x with a configurable step.
- **Per-site speed rules** — set a default playback speed for specific domains
  (for example, always 2x on lecture sites).
- **Per-site disabling** — turn the controller off on sites where you do not want it.
- **Remember speed** — optionally keep your last used speed across sessions and tabs.
- **Speed fightback** — automatically reapply your speed when a site's player tries to reset it.
- **Draggable overlay** — drag the speed indicator anywhere over the video.
- **Fully customizable shortcuts** — remap every key, add modifier combinations
  (Ctrl, Shift, Alt), and create multiple preferred-speed toggles.
- **Custom controller CSS** — style or reposition the overlay with your own CSS rules.

## Default keyboard shortcuts

- **S** — decrease playback speed
- **D** — increase playback speed
- **R** — reset playback speed to 1.0x
- **Z** — rewind 10 seconds
- **X** — advance 10 seconds
- **G** — toggle between the current speed and the preferred speed
- **V** — show/hide the controller
- **M** — set a marker at the current position
- **J** — jump back to the previously set marker

Every shortcut is fully customizable on the extension's options page. You can reassign keys, add modifier combinations, and define multiple preferred-speed shortcuts with different values for quick switching. Click **Add** in the settings to create more bindings. Refresh the page after changing them for the new bindings to take effect.

## Changes in this fork

Based on upstream v0.11.1. No upstream feature, shortcut, or setting has been removed or altered.

**Added**

- **Transient overlay on speed / pause shortcuts** — pressing the increase-speed, decrease-speed, or pause shortcut now reveals the speed overlay automatically, and it hides itself again after the number of seconds configured under "Auto-hide". Upstream only changes overlay visibility from the key bound to "show/hide controller".
- **"Auto-hide" setting** — on the "Advanced" tab of the options page, controls how many seconds the overlay stays visible after such a shortcut. Fractional values are accepted; the default is 3 seconds.

**Changed**

- **Explicit hide no longer suppresses transient feedback** — upstream, if "start hidden" was enabled or the user had pressed the hide key, speed / pause shortcuts would not reveal the overlay. This fork keeps that transient feedback visible regardless; only unavailable media makes the overlay fully invisible. No other overlay behavior was changed.
- **Flash duration is now configurable** — upstream hard-coded 2 seconds; this fork reads the "Auto-hide" setting instead (default 3 seconds).
- **UI localization** — options page, popup, and this documentation are translated into Simplified Chinese.

**Fixed**

- **Mojibake on the options and popup pages** — those pages were missing `<meta charset="utf-8">`, so browsers running under a Chinese locale fell back to GBK decoding and rendered the Chinese text as garbage. The encoding declaration has been added.

## License

(MIT License) - Copyright (c) 2014 Ilya Grigorik  
Copyright (c) 2026 thomasfan (Simplified Chinese localization and modifications)

[chrome-web-store-version]: https://img.shields.io/chrome-web-store/v/nffaoalbilbmmfgbnbgppjihopabppdk?label=Chrome%20Web%20Store
[chrome-web-store-users-badge]: https://img.shields.io/chrome-web-store/users/nffaoalbilbmmfgbnbgppjihopabppdk
[chrome-web-store-stars]: https://img.shields.io/chrome-web-store/stars/nffaoalbilbmmfgbnbgppjihopabppdk
[github-release-badge]: https://img.shields.io/github/v/release/igrigorik/videospeed
[chrome-web-store-link]: https://chromewebstore.google.com/detail/video-speed-controller/nffaoalbilbmmfgbnbgppjihopabppdk
[github-release-link]: https://github.com/igrigorik/videospeed/releases
[upstream-link]: https://github.com/igrigorik/videospeed
