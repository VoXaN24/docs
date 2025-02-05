# Installer et configurer OpenLDAP

Dans un premier temps il faut installer OpenLDAP

```
sudo apt install slapd ldap-utils
```

## Configuration

On commence directement la configuration

On commence par définir notre mot de passe administrateur de l'annuaire LDAP

<figure><img src="../.gitbook/assets/image (45).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (46).png" alt=""><figcaption></figcaption></figure>

On va maintenant faire notre configuration de notre serveur OpenLDAP

```bash
sudo dpkg-reconfigure slapd
```

<figure><img src="../.gitbook/assets/image (37).png" alt=""><figcaption></figcaption></figure>

On choisi "Non" Pour justement faire la configuration de OpenLDAP

On choisi notre domaine, cela sera le même pour toute les machines présente sur le réseau

<figure><img src="../.gitbook/assets/image (38).png" alt=""><figcaption></figcaption></figure>

On choisi le nom de notre organisation

<figure><img src="../.gitbook/assets/image (39).png" alt=""><figcaption></figcaption></figure>

On reconfigure le mot de passe Adminstrateur

<figure><img src="../.gitbook/assets/image (40).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../.gitbook/assets/image (41).png" alt=""><figcaption></figcaption></figure>

On ne supprime pas la base de donnée

<figure><img src="../.gitbook/assets/image (42).png" alt=""><figcaption></figcaption></figure>

Pour éviter tout problèmes on déplace l'ancienne base de donnée

<figure><img src="../.gitbook/assets/image (43).png" alt=""><figcaption></figcaption></figure>

Et voila ! OpenLDAP est installé !

<figure><img src="../.gitbook/assets/image (44).png" alt=""><figcaption></figcaption></figure>
