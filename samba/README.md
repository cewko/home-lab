# samba

```
sudo apt update
sudo apt install samba

mkdir -p /srv/storage/share
mkdir -p /srv/storage/obsidian

sudo chown -R $USER:$USER /srv/storage/share /srv/storage/obsidian
chmod -R 770 /srv/storage/share /srv/storage/obsidian

sudo smbpasswd -a $USER

sudo cp /etc/samba/smb.conf /etc/samba/smb.conf.bak
sudo nano /etc/samba/smb.conf

[share]
   path = /srv/storage/share
   browseable = yes
   read only = no
   valid users = your_username
   create mask = 0660
   directory mask = 0770

[obsidian]
   path = /srv/storage/obsidian
   browseable = yes
   read only = no
   valid users = your_username
   create mask = 0660
   directory mask = 0770

sudo systemctl restart smbd

sudo ufw allow Samba
```
