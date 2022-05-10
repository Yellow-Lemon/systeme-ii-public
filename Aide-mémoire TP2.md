# TP2 Système


* [Commande utile](#commande-utile) 
* [Création de la machine](#création-de-la-machine-virtuelle)
* [Mise à jour machine](#mise-à-jour-machine)
* [Interaction machine locale / machine remote](#interaction-machine-locale--machine-remote)
* [Clé SSH](#création-des-clés-ssh)
* [Docker & Nginx](#docker--nginx)
* [Ouvrir les ports](#ouvrir-undes-ports)
* [Gestion d'utilisateurs et groupes](#gestion-utilisateurs-et-groupes)
* Reverse proxy
* DNS
* dav
* ftp
* Cron et backup


<!--DOCKER : https://medium.com/warp9/deploying-a-static-website-in-a-docker-container-f6b7d8eed15f -->
---

## Commande utile
Connection machine ssh
```
ssh USERNAME@IP
```
Connection machine avec clé ssh
```
ssh -i <private key path> USERNAME@IP
```

Exécuter une commande en administrateur :
```
sudo COMMANDE
```
Passer sur root :
```
sudo su -
```
Passer sur un autre user :
```
sudo su USERNAME
```
Voir si un port est utilisé :
```
sudo lsof -i :PORT
```

`~` = répertoire personnel

`$` = utilisateur normal\
`#` = root

[commande copier :](https://www.educba.com/copy-command-in-linux/)
```
cp SOURCE DESTINATION
```

Pour gérer une application (Démarrer, arrêter...)
```
sudo systemctl status APPLICATION (voir l'état)
sudo systemctl start APPLICATION
sudo systemctl restart APPLICATION
sudo systemctl stop APPLICATION
sudo systemctl enable APPLICATION (Lancer au démarrage)
sudo systemctl disable APPLICATION
```
Pour print le contenu d'un site dans la console :
```
curl IP
```

---
## Création de la machine virtuelle
https://www.youtube.com/watch?v=ADdGZEfmNzQ&t=1075s

---
## Mise à jour machine
Télécharger et installer les mises à jour :
```
sudo apt update
sudo apt upgrade
```
Redémarrer :
```
sudo reboot
```
---
## Interaction machine locale / machine remote
Copier de la machine locale vers la machine remote
```
scp FILENAME USERNAME@IP:/DESTINATION
```
Exemple
```
scp index.html lemon@1.2.3.4:/home/lemon/html
```
Copier de la machine remote à la machine locale :
```
scp USERNAME@IP:FILENAME DESTINATION
```
`-r` permet de copier des dossiers

---
## Création des clés SSH
<!--ssh-keygen -t rsa-->
<!-- https://www.youtube.com/watch?v=vSvNBmZN548 -->
### 1. Générer les clées
Dans le cmd, sur la machine locale :
```
ssh-keygen 
```
Localisation des clés (par défaut) :
`C:\Users\USERNAME\.ssh`

`id.rsa` = clé privée\
`id.rsa.pub` = clé publique

### 2. Copier la clé sur la machine remote
Copier la clé publique (tout le contenu de `.pub`) dans le dossier `authorized_keys` sur la machine remote.

Sur la machine remote, les clés authorisées se trouvent à : `~/.ssh/authorized_keys`

Pour tester, se reconnecter à la machine :
```
ssh USERNAME@LOCALHOST
```
Si ça ne demande pas de mdp c'est bon

---
## Docker & Nginx
[Vidéo youtube](https://www.youtube.com/watch?v=mgwo8fq-SkA)\
[Plus d'info sur les commandes](https://phoenixnap.com/kb/docker-run-command-with-examples)

Installer Docker
```
sudo apt install docker.io
```
Télécharger l'image nginx pour docker :
```
sudo docker pull nginx:latest
```
Lister les container en cours d'exécution :
```
docker ps
```
Pour tout voir (incluant stoppé) :
```
docker ps -a
```
Build et run un container (commande de base):
```
docker run IMAGE
```
attribut utile sur la commande `run` :
```
-p PORTLOCAL:PORTCONTAINER 
-d (Pour run le container en arrière plan)
--name (Pour donner un nom au container (peut-être utilisé au lieu du ID))
-v (définir le volume (se met à jour automatiquement))
```
Arrêter un container :
```
docker stop ID
```
Supprimer un container :
```
docker rm ID
```

## Ouvrir un/des port(s)
https://docs.microsoft.com/en-us/azure/virtual-machines/windows/nsg-quickstart-portal

HTTP = 80 \
HTTPS = 443

---
## Gestion utilisateurs et groupes
Créer un user
```
sudo adduser USERNAME
```
`--force-badname` pour un nom qui ne respecte pas les critères

Rendre un user sudo :
```
sudo usermod -aG sudo USERNAME
```


