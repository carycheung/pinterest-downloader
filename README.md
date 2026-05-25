# Pinterest Downloader

A zero-backend, single-file web app to batch download videos and original-size images from Pinterest. Runs entirely in your browser.

**🔗 Live: https://carycheung.github.io/pinterest-downloader/**

## Features

- Paste many Pinterest URLs (one per line) and parse them in parallel
- Supports both `pinterest.com/pin/...` and `pin.it/...` short links
- Smart video variant dedup — picks H.264 + highest resolution automatically
- Per-card preview: playable video with duration, image with dimensions, file size after download
- Bulk select / select videos only / select images only
- Direct write to a chosen folder (Chrome/Edge/Arc via File System Access API)
- ZIP packaging fallback for all browsers
- No server, no tracking, no analytics — pure HTML/CSS/JS in one file

## How it works

The page fetches each Pinterest pin URL through a public CORS proxy, scans the response HTML for `i.pinimg.com` (images) and `v.pinimg.com` (videos) URLs, deduplicates by file hash, and downloads each blob via either the File System Access API or the browser's native download flow. Nothing leaves your machine except the proxied request to Pinterest.

## Local use

Just open `index.html` in your browser.

## Limitations

- Public CORS proxies (codetabs / corsproxy / allorigins) occasionally rate-limit or go down. Retry usually works.
- File size cannot be predicted before download — Pinterest CDN doesn't expose `Content-Length` through proxies.
- Story pins / carousel pins may return only the first slide.
- HLS-only videos aren't supported in pure browser JS.

For long-term stability, swap the proxies in `index.html` with your own [Cloudflare Worker](https://developers.cloudflare.com/workers/) — takes 5 minutes and gives you unlimited free requests.

## License

MIT
