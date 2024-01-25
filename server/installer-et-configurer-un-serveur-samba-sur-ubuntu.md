# Installer et Configurer un serveur samba sur Ubuntu

1. Installer samba

```
apt update
apt install samba
```

2. Crée le fichier de configuration de votre partage ( `/etc/samba/smb.conf` )

```
[sambashare]
    comment = Samba on Ubuntu
    path = <folder>
    read only = no
    browsable = yes
```

3. Redémarrer Samba

```
sudo service smbd restart
```

4. Allouer le trafic vers SMB

```
sudo ufw allow samba
```

5. Crée un utilisateur pour votre partage

```
adduser <user>
smbpasswd -a <user>
```
