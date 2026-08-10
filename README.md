# shorts-media

Static hosting for rendered short-form videos, served via GitHub Pages so
scheduling tools (Buffer) can fetch them by URL at publish time.

## Why this exists

Buffer does not download the video when a post is created — it fetches it at
publish time, which can be hours or days later. This was previously served
from Cloudflare "quick tunnels", which explicitly carry no uptime guarantee.
They died repeatedly (QUIC transport failures, DNS registration failures,
laptop sleep), and because each restart produces a *new* hostname, every
already-scheduled post silently broke and published as a 0-second video.

GitHub Pages gives a permanent URL, a real CDN, the correct `video/mp4`
content type, and no dependence on any machine here being awake or reachable.

Files are named `<episode-slug>.mp4` and served from:

    https://neguscho.github.io/shorts-media/<episode-slug>.mp4
