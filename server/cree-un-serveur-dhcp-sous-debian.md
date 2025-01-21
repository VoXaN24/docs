# Crée un serveur DHCP sous Débian

### Installation de DHCP

Pour installer un serveur DHCP il faut installer le paquet `isc-dhcp-server`

<pre class="language-bash"><code class="lang-bash"><strong>apt install isc-dhcp-server
</strong></code></pre>

<figure><img src="../.gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure>

⚠️ Ne pas lancer le serveur DHCP ⚠️\
\


## Configuration du serveur DHCP

#### Récupération de l'interface de notre carte réseau grace a la commande `ip a`

<figure><img src="../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>

Ici dans mon cas mon interface pour le DHCP c'est `ens256`

#### Fichier de configuration

Dans un premier temps on va modifier le fichier `/etc/default/isc-dhcp-server`

```bash
nano /etc/default/isc-dhcp-server
```

Décommenté la ligne `DHCPDv4_CONF=/etc/dhcp/dhcpd.conf`

Et on renseigne nos interface

```
INTERFACESv4="ens256"
INTERFACESv6="ens256"
```

Dans mon cas c'est `ens256`

<figure><img src="../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>

#### On va modifier maintenant le fichier **`/etc/dhcp/dhcpd.conf`**

```
# Bail de 24H
default-lease-time 86400; 
# Bail maxi de 48H
max-lease-time 172800; 
# Domaine
option domain-name     "vm.local";
 
# Déclaration d'un réseau
subnet 192.168.1.0 netmask 255.255.255.0 {
        range                           192.168.1.100 192.168.1.199; # Plage IP
        option domain-name-servers      1.1.1.1; # DNS Cloudflare
        option routers                  192.168.1.1; # Passerelle
}
 
```



<figure><img src="../.gitbook/assets/image (21).png" alt=""><figcaption></figcaption></figure>
