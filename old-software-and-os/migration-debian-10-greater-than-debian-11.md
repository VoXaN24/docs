---
description: Migré votre machine sous Debian 10 vers Debian 11 en moins de 10 minutes !
---

# Migration Debian 10 -> Debian 11

1. Faite une backup de votre machine, mettez a jour Debian 10 jusqu'au bout et redémarrer la machine
2. Modifier le fichier `/etc/apt/sources.list` avec un éditeur de texte (ex. nano) et remplacer **buster** par **bullseye** et **buster/updates** par **bullseye-security**\
   ![Ancien Source.list](<../.gitbook/assets/image (17).png>)\
   _(Ancien sources.list)_\
   ![Nouveau sources.list](<../.gitbook/assets/image (4) (2).png>)\
   &#xNAN;_(Nouveau sources.list)_
3. Mettez a jour la liste des paquet une fois les dépots changer avec `sudo apt update`
4. Faite une premiere vague de mise a jour avec `sudo apt upgrade --without-new-pkgs`
5. Puis mettez a jour votre systéme avec : `sudo apt full-upgrade`
6. Redémarrez et vous voila sous Debian 11 !

