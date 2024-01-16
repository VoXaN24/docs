---
description: Pour bannir efficacement les BOTS !
---

# Intégré Nginx Proxy Manager à fail2ban

Prérequis : \
\- Avoir Fail2ban d'installer\
\- Avoir son dossier de log monté en dehors du conteneur docker de NPM ([Ligne à ajouté au docker compose](https://paste.voxhost.fr/?ab8aa48e9bb5dc75#8AxSLxSjJncY1QpMcND2eeAdo3Z7uVf2gtFrXLrhphYL) )

### 1 . Crée le fichier `/etc/fail2ban/filter.d/npm.conf`

```
[INCLUDES]

[Definition]

failregex = ^<HOST>.+" (4\d\d|3\d\d) (\d\d\d|\d) .+$
            ^.+ 4\d\d \d\d\d - .+ \[Client <HOST>\] \[Length .+\] ".+" .+$
```

### 2. Crée le ficher `/etc/fail2ban/action.d/docker-action.conf`

```
[Definition]

actionstart = iptables -N f2b-npm-docker
              iptables -A f2b-npm-docker -j RETURN
              iptables -I FORWARD -p tcp -m multiport --dports 0:65535 -j f2b-npm-docker

actionstop = iptables -D FORWARD -p tcp -m multiport --dports 0:65535 -j f2b-npm-docker
             iptables -F f2b-npm-docker
             iptables -X f2b-npm-docker

actioncheck = iptables -n -L FORWARD | grep -q 'f2b-npm-docker[ \t]'

actionban = iptables -I f2b-npm-docker -s <ip> -j DROP

actionunban = iptables -D f2b-npm-docker -s <ip> -j DROP
```

### 3. Crée le fichier `/etc/fail2ban/jail.d/npm.local`

```
[npm]
enabled = true
chain=INPUT
maxretry = 3
bantime = 48h
findtime = 60m
logpath = /path/to/logs/default-host_*.log #Changer les chemins pour être en accord avec où sont vos logs
          /path/to/logs/proxy-host-*.log
action = docker-action
```

### 4. Redémarrer fail2ban !

```
sudo systemctl reload fail2ban.service
```
