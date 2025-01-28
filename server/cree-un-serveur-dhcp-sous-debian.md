# Crée un serveur DHCP sous Débian

Installation de DHCP

Pour installer un serveur DHCP il faut installer le paquet `isc-dhcp-server`

<pre class="language-bash"><code class="lang-bash"><strong>apt install isc-dhcp-server
</strong></code></pre>

<figure><img src="../.gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure>

⚠️ Ne pas lancer le serveur DHCP ⚠️\
\


## Configuration des interface sur notre machine

Récupération de l'interface de notre carte réseau grâce à la commande `ip a`

<figure><img src="../.gitbook/assets/image (5).png" alt=""><figcaption><p>Retours de la commande ip a</p></figcaption></figure>

Ici, ma carte réseau sera `ens37`, mais je peux aussi utilisé son nom alternatif `enp2s5`

On doit renseigner l'IP de la carte réseau à l'avance en modifiant le fichier `/etc/network/interfaces`

Dans mon cas, mon réseau aura pour bloc IP `172.16.0.0/16` et mon interface : `ens37`

```
# DHCP
auto ens37
iface ens37 inet static
 address 172.16.0.1 #Address de votre serveur DHCP
 netmask 255.255.0.0 #Masque de sous réseau, dans mon cas IP de classe B
 dns-nameservers 172.16.0.1 #Serveur DNS, vous pouvez ne pas en renseigné ou renseigné votre DNS Interne ou un DNS Publique
```

<figure><img src="../.gitbook/assets/image (32).png" alt=""><figcaption></figcaption></figure>

On redémarre la machine pour que la configuration s'applique

```
sudo shutdown -r now
```

Et voila on a notre IP !\


<figure><img src="../.gitbook/assets/image (24).png" alt=""><figcaption></figcaption></figure>

## Configuration du serveur DHCP

#### Récupération de l'interface de notre carte réseau grâce a la commande `ip a`

<figure><img src="../.gitbook/assets/image (25).png" alt=""><figcaption></figcaption></figure>

Ici dans mon cas mon interface pour le DHCP c'est `ens37`

#### Fichier de configuration

Dans un premier temps on va modifier le fichier `/etc/default/isc-dhcp-server`

```bash
nano /etc/default/isc-dhcp-server
```

Décommenté la ligne `DHCPDv4_CONF=/etc/dhcp/dhcpd.conf`

Et on renseigne nos interface

```
INTERFACESv4="ens37"
#INTERFACESv6="ens37" il est commenté car je n'ai pas d'IPv6
```

Dans mon cas c'est `ens37`

<figure><img src="../.gitbook/assets/image (4) (1).png" alt=""><figcaption></figcaption></figure>

#### On va modifier maintenant le fichier **`/etc/dhcp/dhcpd.conf`**

```
# Bail de 24H
default-lease-time 86400; 
# Bail maxi de 48H
max-lease-time 172800; 
# Domaine
option domain-name     "vm.local";
 
# Déclaration d'un réseau
subnet 172.16.0.0 netmask 255.255.0.0 {
        range                           172.16.0.100 172.16.255.250; # Plage IP
        option domain-name-servers      1.1.1.1; # DNS Cloudflare
        option routers                  172.16.0.1; # Passerelle
}
 
```

![](<../.gitbook/assets/image (30).png>)

Et on active et démarre le service&#x20;

<figure><img src="../.gitbook/assets/image (23).png" alt=""><figcaption></figcaption></figure>

Pour rallier une autre machine, vous devez juste la mettre sur le même réseau et activé le DHCP

<figure><img src="../.gitbook/assets/image (27).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (31).png" alt=""><figcaption></figcaption></figure>
