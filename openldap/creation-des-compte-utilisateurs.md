---
description: On va crée nos utilisateur pour notre serveur LDA
hidden: true
---

# Création des compte utilisateurs

## Création de notre fichier racine

Pour commencer, on va crée notre fichier racine

```bash
nano /etc/ldap/racine.ldif
```

On va donc crée notre racine, ou "DN" (Distinguished Name)

Comment se décompose se fichier ? Voila un petit exemple !

<figure><img src="https://i.hessfr.fr/NIba7/NeFuYEHe46.png/raw" alt=""><figcaption><p>Contenu du fichier racine.ldif</p></figcaption></figure>

1ére ligne : `dn: dc=vmldap,dc=lan` -> Cela correspond au nom de notre racine (ici vmldap) et de son extension (ici lan)

2nd ligne et 3éme ligne : `objectClass: organistation` & `objectClass : dcObject` -> Cela veut dire ue l'objet de classe qu'on veut utiliser est une organisation

4éme ligne : `o: Hessfr` --> Défini le nom de l'organisation (ici Hessfr)

5éme ligne: `dc: Hessf`r --> Défini le nom de la base (ici Hessfr)

Maintenant, on ajoute le fichier racine.ldif à notre annuaire ldap

La commande à utilisé est :

```bash
ldapadd -x -D "cn=admin,dc=<nom de votre base>,dc=td" -W -f racine.ldif
```

Dans mon cas la commande est donc

```bash
ldapadd -x -D "cn=admin,dc=Hessfr,dc=td" -W -f racine.ldif
```



