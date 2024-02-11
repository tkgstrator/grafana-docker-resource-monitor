## Grafana Docker Resource Monitor

### Requirements

- Docker
- Docker compose
- [Cloudflare Zero Trust Tunnel Token](https://one.dash.cloudflare.com/)

Create a tunnel in `Networks -> Tunnels`, and select Cloudflared as connecter and save it. Then, choose the environment you want to use and copy it.

## Installation

```zsh
git clone https://github.com/tkgstrator/grafana-docker-resource-monitor.git
cd grafana-docker-resource-monitor
```

Copy and edit `TUNNEL_TOKEN` in .env.

```zsh
cp .env.example .env
vi .env
```

Launch!

```zsh
docker compose up -d
```

### Cloudflare Tunnel

Select the tunnel and set Public hostnames like below.

- Subdomain: `YOUR_SUBDOMAIN` you want, like a `grafana`.
- Domain: Choose `YOUR_DOMAIN` managed on Cloudflare.
- Type: `HTTP` // Do not change it
- URL: `grafana:3000` // Do not change it

Then you can see the visualized analytics on `https://YOUR_SUBDOMAIN.YOURDOMAIN` in the browser.
