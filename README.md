# whoami-static

Static-site clone of my [whoami](https://infdxeta.info/whoami/) profile page, built for
free hosting on Netlify.

The original lives in a Docker container on my BananaPi (nginx + a small shell script
that writes a live `uptime.txt` file, exposed externally via Cloudflare). This clone
drops everything container/host-specific and keeps only what a static host needs:

| Original | This repo |
|---|---|
| `index.html`, `style.css`, `klept.ico` | Copied as-is |
| `entrypoint.sh` writing `uptime.txt` server-side every 5s, polled by the page | Replaced with a small inline script that computes elapsed time client-side from a fixed launch instant - no server needed, same live-ticking footer |
| `Dockerfile`, `docker-compose.yml`, `default.conf`, `health.txt`, `monitoring/` | Not included - container health checks and the systemd watchdog that restarts the container are specific to self-hosting on the BananaPi and don't apply to Netlify |

## Deploying

No build step - it's plain HTML/CSS/JS. Connect this repo in Netlify with:

- Build command: *(none)*
- Publish directory: `.`

`netlify.toml` already declares this, so Netlify should pick it up automatically once
the repo is connected.
