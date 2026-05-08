# uptime-kuma

```
mkdir -p /srv/compose/uptime-kuma
mkdir -p /srv/data/uptime-kuma
cd /srv/compose/uptime-kuma

nano compose.yml

services:
  uptime-kuma:
    container_name: uptime-kuma
    image: louislam/uptime-kuma:2
    hostname: uptime-kuma
    restart: unless-stopped

    ports:
      - "3001:3001/tcp"

    volumes:
      - /srv/data/uptime-kuma:/app/data

docker compose up -d
```
