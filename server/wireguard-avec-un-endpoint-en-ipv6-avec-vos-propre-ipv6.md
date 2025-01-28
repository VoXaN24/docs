---
description: >-
  Comment crée son propre VPN avec comme point d'entrer une IPv6, et en sortie
  de l'IPv4/IPv6 !
---

# Wireguard avec un endpoint en IPv6 (Avec vos propre IPv6 !)

Pour cette exemple je vais utiliser une machine herberger sur Microsoft Oracle Cloud et Ubuntu 20.04 LTS, pensez a vérifier si votre hébergeur posséde sont propre pare-feu et d'ouvrir les port.

### I/ Récuperer votre bloc d'adresse Ip sur tunnelbroker

1. Inscrivez vous sur [TunnelBroker.net](https://tunnelbroker.net/)
2. Crée un tunnel dans la région la plus proche de votre serveur qui vous servira de vps (Ici au Pays Bas)

![Home page](<../.gitbook/assets/image (11).png>)

![Choix du pays du tunnel](<../.gitbook/assets/image (13).png>)

![Voila votre bloc d'IPv6](<../.gitbook/assets/image (10) (2).png>)

3\. Application de vos IPv6 a votre serveur.

(Si vous herbergeur propose des IPv6, Merci de les supprimer de votre configuration réseau)

* Allez dans "Exemple Configurations" -> Votre OS

![](<../.gitbook/assets/image (2) (1) (2).png>)

* Copier la configuration dans `/etc/network/interfaces` &#x20;
* Si vous avez (comme moi) netplan, ce n'est pas si simple...

Vous allez devoir crée 3 fichier :&#x20;

\-- **`/etc/systemd/network/he-ipv6.network`**

```
[Match]

[Network]
Tunnel=he-ipv6
```

\-- **`/etc/systemd/network/he-ipv6-tunnel.netdev`**

```
[Match]                                                                                                                                                                                                            

[NetDev]                                                                                                                                                                                                           
Name=he-ipv6                                        
Kind=sit                                            

[Tunnel]
Independent=true                                            
Local=x.x.x.x #Votre IP Privé si le serveur est dans un NAT, sinon votre IP Publique                                  
Remote=x.x.x.x #L'IPv4 du TunnelBroker                         
TTL=255
```

\-- **/etc/netplan/yourconfigname.yaml (A ajouté a votre configuration)**

```
# This file describes the network interfaces available on your system
# For more information, see netplan(5).
network:
  version: 2
  renderer: networkd
  ethernets:
      he-ipv6:
          dhcp4: no
          dhcp6: no
          addresses: ['2001:470:xxx:xxx::2/64']
          gateway6: 2001:470:xxx:xxx::1
      enp0s3:
      ...
```

**executer la commande :** `systemctl restart systemd-networkd && netplan apply`

Et voila votre serveur a de l'IPv6 !

![Test de ping sur google](<../.gitbook/assets/image (12).png>)

### II/ Installation du serveur wireguard

1. Verifiez que votre serveur a bien les derniére mise a jours
2.  Installer les paquet suivant :&#x20;

    ```
    wireguard wireguard-tools resolvconf bash curl wget
    ```



![](<../.gitbook/assets/image (3) (1) (1) (1).png>)

3\. On va utiliser un petit script interactif :&#x20;

```
curl -O https://raw.githubusercontent.com/angristan/wireguard-install/master/wireguard-install.sh
chmod +x wireguard-install.sh
bash wireguard-install.sh
```

![](<../.gitbook/assets/image (15).png>)

4\. Crée votre premier client :&#x20;

![](<../.gitbook/assets/image (10).png>)



Vous avez plus qu'a vous connecter via le client wireguard !
