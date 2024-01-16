# Intégré Caddy à fail2ban

### 1. Crée le fichier `/etc/fail2ban/filter.d/caddy-status.conf`

```
[Definition]
failregex = ^.*"remote_ip":"<HOST>",.*?"status":(?:401|403|500),.*$
ignoreregex =
datepattern = LongEpoch
```

Cela va permettre de filtrer les requette qui tombe en erreur 401/403 et 500

### 2. Crée le fichier `/etc/fail2ban/jail.d/caddy.conf`

```
[caddy-status]
enabled     = true
port        = http,https
filter      = caddy-status
logpath     = /var/log/caddy/*.access.log
maxretry    = 10
```

### 3. Redémarrer fail2ban

```
sudo systemctl reload fail2ban.service
```
