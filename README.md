# Pinterest Downloader

A zero-backend, single-file web app to download videos and original-size images from Pinterest. Runs entirely in your browser.

**Live demo**: https://YOUR_USERNAME.github.io/pinterest-downloader/

## Features

- Paste a Pinterest URL (`pinterest.com/pin/...` or `pin.it/...` short links)
- Extracts 720p MP4 videos and original-resolution images
- Multiple CORS proxy fallbacks
- No server, no tracking — pure HTML/CSS/JS in one file
- Free hosting on GitHub Pages

## How it works

The page fetches the Pinterest pin URL through a public CORS proxy, parses the embedded `__PWS_DATA__` JSON for media URLs, then downloads the file as a Blob via the browser's native download flow. Nothing leaves your machine except the proxied request to Pinterest.

## Deploy to GitHub Pages

1. Create a new GitHub repo (e.g. `pinterest-downloader`), public.
2. Push this folder to it:
   ```bash
   git init
   git add .
   git commit -m "init"
   git branch -M main
   git remote add origin https://github.com/YOUR_USERNAME/pinterest-downloader.git
   git push -u origin main
   ```
3. On GitHub: **Settings → Pages → Source: Deploy from branch → main / root → Save**.
4. Wait ~1 minute, your site is live at `https://YOUR_USERNAME.github.io/pinterest-downloader/`.

## Local use

Just open `index.html` in your browser. That's it.

## Limitations

- Public CORS proxies (corsproxy.io / allorigins / codetabs) occasionally rate-limit or go down. If parsing fails, retry — the app falls back through three proxies automatically.
- Story pins and some carousel pins return only the first slide.
- HLS-only videos (rare on Pinterest) aren't supported in pure browser JS.

If proxies become a problem long-term, swap `CORS_PROXIES` in `index.html` with your own [Cloudflare Worker](https://developers.cloudflare.com/workers/) — takes 5 minutes and gives you unlimited free requests.

## License

MIT
