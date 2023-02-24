# SAE 4.01 - Docker
Ce repository à était crée pour crée toute une architecture sous docker pour la SAE 4.01 du BUT Informatique de l'IUT de Montpellier/Sète


## Parties
   - 1/ Informations importantes
   - 2/ Prérequis
   - 3/ Configuration
   - 4/ Executer les containers
   - 4/ PostgreSQL & SIG
   - 5/ Test

## 1/ Informations importantes
Suite à ce tutoriel sous docker vous pourai accedez à vos services en utiliser les port suivants:
 - **Apache:** 8082
 - **PostgreSQL:** 5432

## 2/ Prérequis
Pour utiliser ce repository il vous faudrat __obligatoirement__ avec installé `Docker` **et** `Docker Desktop` sur votre machine

### Installation de Docker sous Windows
Vous pouvez suivre ce lien, qui vous expliquera comment installer Docker sur votre machine window: https://docs.docker.com/desktop/install/windows-install/

### Installation de Docker sous MacOS (*Processeur: Intel*)
Vous pouvez suivre le lien suivant (*Partie Intel*): https://docs.docker.com/desktop/install/mac-install/ <br/>
Puis vous devez télécharger et installer 'Docker Desktop' avec ce lien: https://desktop.docker.com/mac/main/amd64/Docker.dmg?utm_source=docker&utm_medium=webreferral&utm_campaign=docs-driven-download-mac-amd64 

### Installation de Docker sous MacOS (*Processeur: ARM*)
Vous pouvez suivre le tutoriel suivant: https://docs.docker.com/desktop/install/mac-install/<br/>
Suite à ça vous devez éxecuter la commande suivante dans votre terminal: `softwareupdate --install-rosetta` <br/>
Et vous venez aussi Télécharger et Installer 'Docker Desktop': https://desktop.docker.com/mac/main/arm64/Docker.dmg?utm_source=docker&utm_medium=webreferral&utm_campaign=docs-driven-download-mac-arm64 

### Installation de Docker sous Linux
Vous pouvez suivre le tutoriel suivant: https://docs.docker.com/desktop/install/linux-install/ <br/><br/>

Suite à votre installation de Docker, vous pouvez cloner le repository et suivre la prochaine étape
<br/>

## 3/ Configuration : 
Suite à l'installation de Docker il vous faut ensuite **configurer** le fichier `.env` <br/>
Pour ceci, vous devrai remplacer les noms donner par défaut `<VOTRE_NOM>` par vos noms de projets <br/>
> Exemple: DB_NAME=romain

<br/>
Fichier .env:

```
DB_NAME=<VOTRE_NOM>
PROJECT_NAME=<VOTRE_NOM>
PROJECT_PATH=/var/www/html
```

## 4/ Executer les containers & Docker :
Docker est une solution de machine virtuelle, c'est grâce à elle que un site peut fonctionner avec le même système sur n'importe qu'elle système d'exploitation (*Window/MacOS/Linux*).<br/>

### Commandes utiles
Pour comprendre comment marche docker, il faut connaitre les commandes essentielles qui sont les suivantes<br/>

`docker ps`: Permet de connaitre les containers en cours d'éxécution<br/>
`docker exec -it <ID_CONTAINER> bash`: Permet de rentrer dans le terminal d'un container<br/>
`docker compose build`: Permet de build le dossier courant<br/>
`docker compose up -d`: Permet d'éxecuter tous les containers du dossier courant<br/>
`docker compose stop`: Permet d'arretêr tous les containers
<br/><br/>

### Instructions

Ensuite vous pouvez suivre les instructions suivantes pour executer vos container docker pour la première fois pour cette SAE.

`cd /path/to/folder/`<br/>
`docker compose build`<br/>
`docker compose up -d`<br/>
`docker ps` *et récupérer l'identifiant du container Apache*<br/>
`docker exec -it <IDENTIFIANT> bash`<br/>
Ensuite il vous suffit d'utilise un linux normal pour clone votre repository dans le dossier `/var/www/html` et vous rendre sur l'adresse `127.0.0.1:8082`<br/>
<br/>

## 5/ PostgreSQL & Postgis
Maintenant que votre serveur Apache est fonctionnel il vous faut que vous installer votre serveur de base de données sur le container postgres !<br/>

### Connexion à PostgreSQL
Pour la connexion à PostgreSQL, vous devez ouvrir DBeaver ou Datagrip et rentrer les identifiants de connexion suivantes:

```
Host: 127.0.0.1
Port: 5432
User: postgres
Password: changeme
Database: postgres
```
<br/>
Une fois arriver sur le serveur de Base de Données il vous suffira de crée un nouvel utilisateur et une nouvelle base de données.

### PostGIS
Pour la SAÉ, il vous est demander d'installer l'extension Postgres qui se nomme PostGIS, pour faire ceci il vous suffit de suivre les instruction suivantes:

1/ Connecter vous au bash de la VM postgres (`docker exec -it <ID_POSTGRES> bash`).
2/ Mettre à jour la machine (`apt update` et `apt upgrade`)
3/ 
