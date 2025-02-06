---
description: >-
  Ce petit tutoriel assez cours va vous permettre de télécharger et installer un
  conteneur LXC sous Proxmox
---

# Crée un conteneur LXC Sur ProxMox



1. Télécharger l'image que vous souhaitez

* Allez à l'endroit où est stocké vos iso et template (Par défaut dans local)

![Promox Panel](<.gitbook/assets/image (10) (1).png>)

* Puis dans CT Modèles -> Template

![Ct Template Panel](<.gitbook/assets/image (4) (1) (1).png>)

* Sélectionner le template que vous souhaitez télécharger

![Ici par exemple Centos 8](<.gitbook/assets/image (1) (1) (1) (1).png>)

* Patienter le temps du téléchargement

![Téléchargement de l'image de CentOS 8](<.gitbook/assets/image (5) (1).png>)

2\. Créer la machine

* Appuyer sur "Créer CT"

![Promox panel](<.gitbook/assets/image (9) (1).png>)

* Rentrer le mot de passe SSH de la machine ou votre clé SSH, Puis configurer comme si vous configuriez une machine virtuel

&#x20;

![Ecran 1](<.gitbook/assets/image (1) (2).png>)

![Choix du template](<.gitbook/assets/image (3) (1) (1) (1) (1).png>)

![taille du disque](<.gitbook/assets/image (8).png>)

![Nombre de coeur du CPU du contener](<.gitbook/assets/image (6) (1).png>)

![choix de la taille de ram et de l'espace swap](<.gitbook/assets/image (11) (1).png>)

![Configuration du réseau](<.gitbook/assets/image (2) (1) (1).png>)

![Configuration des DNS](<.gitbook/assets/image (7).png>)

![Récapitulation](<.gitbook/assets/image (14) (1).png>)

* Patienter un petit moment après appuyer sur Terminé

![](<.gitbook/assets/image (12) (1).png>)

* Et voila votre conteneur est en fonctionnement

![](<.gitbook/assets/image (13) (1).png>)
