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

If docker installed by `snap` instead of `apt`, launch is failed with the error of `Error response from daemon: error while creating mount source path '/var/lib/docker': mkdir /var/lib/docker: read-only file system`. In case, you have to change the volumes of cadvisor to `/var/snap/docker/common/var-lib-docker:/var/snap/docker/common/var-lib-docker` from `/var/lib/docker/:/var/lib/docker:ro`.

Also, you can check which package manager you installed docker with the following command `which docker`.

### Cloudflare Tunnel

Select the tunnel and set Public hostnames like below.

- Subdomain: `YOUR_SUBDOMAIN` you want, like a `grafana`.
- Domain: Choose `YOUR_DOMAIN` managed on Cloudflare.
- Type: `HTTP` // Do not change it
- URL: `grafana:3000` // Do not change it

Then you can see the visualized analytics on `https://YOUR_SUBDOMAIN.YOURDOMAIN` in the browser.

## Known issues

- Public dashboard is not available through cloudflared tunnel due to api return Internal Server Error 500.

## References

- [Run Grafana Docker image](https://grafana.com/docs/grafana/latest/setup-grafana/installation/docker/)
- [Configure a Grafana Docker image](https://grafana.com/docs/grafana/latest/setup-grafana/configure-docker/)
- [Docker Container Monitoring with cAdvisor, Prometheus, and Grafana using Docker Compose](https://medium.com/@sohammohite/docker-container-monitoring-with-cadvisor-prometheus-and-grafana-using-docker-compose-b47ec78efbc)
