# backups

```bash
sudo nano /root/.restic-password
sudo chmod 600 /root/.restic-password

sudo mkdir -p /mnt/backups/restic
sudo restic -r /mnt/backups/restic --password-file /root/.restic-password init

sudo nano /usr/local/sbin/homelab-backup


#!/usr/bin/env bash

set -euo pipefail

REPO="/mnt/backups/restic"
PASSWORD_FILE="/root/.restic-password"

if [ ! -f "$REPO/config" ]; then
  echo "restic repo not found at $REPO"
  exit 1
fi

restic -r "$REPO" \
  --password-file "$PASSWORD_FILE" \
  backup /srv/data /srv/storage/obsidian

restic -r "$REPO" \
  --password-file "$PASSWORD_FILE" \
  forget \
  --keep-last 7 \
  --keep-weekly 4 \
  --keep-monthly 6 \
  --prune



sudo chmod 700 /usr/local/sbin/homelab-backup
sudo nano /etc/systemd/system/homelab-backup.service


[Unit]
Description=homelab restic backups

[Service]
Type=oneshot
ExecStart=/usr/local/sbin/homelab-backup


sudo nano /etc/systemd/system/homelab-backup.timer


[Unit]
Description=run homelab backup daily

[Timer]
OnCalendar=*-*-* 03:00:00
Persistent=true

[Install]
WantedBy=timers.target


sudo systemctl daemon-reload
sudo systemctl enable --now homelab-backup.timer


systemctl list-timers | grep homelab
```
