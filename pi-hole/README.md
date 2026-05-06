# pi-hole

```
mkdir -p /srv/data/pi-hole/etc-pihole/
mkdir -p /srv/compose/pi-hole/ && cd /srv/compose/pi-hole/
cp ~/home-lab/pi-hole/compose.yml .
cp ~/home-lab/pi-hole/.env.example . && mv .env.example .env

# fill the values inside .env
nano .env

chmod 600 .env
docker compose up -d
```