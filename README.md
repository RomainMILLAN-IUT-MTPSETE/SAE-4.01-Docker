# Docker - TP2
Ce dépôt à était crée pour le TP 2 du cours de Virtualisation.<br/>
Dépôt crée par Romain MILLAN et Geoffrey PIERRE

<br/>

## Parties
   - 1/ Informations importantes
   - 2/ Prérequis
   - 3/ Executer les containers
   - 4/ PostgreSQL & SIG

<br/>

## 1/ Informations importantes
Suite à ce tutoriel sous Docker, vous pourrez accéder à vos services en utilisant les ports suivants :
 - **Apache:** 8082
 - **PostgreSQL:** 5432
 - **PGAdmin:** 5050

<br/>

## 2/ Prérequis
Pour utiliser ce dépôt, il vous faudra **obligatoirement** avoir installé `Docker` et `Docker Desktop` sur votre machine.

### Installation de Docker sous Windows
Vous pouvez suivre ce lien, qui vous expliquera comment installer Docker sur votre machine Windows: https://docs.docker.com/desktop/install/windows-install/

### Installation de Docker sous MacOS (*Processeur: Intel*)
Vous pouvez suivre le lien suivant (Partie Intel): https://docs.docker.com/desktop/install/mac-install/ <br/>
Puis vous devez télécharger et installer 'Docker Desktop' avec ce lien: https://desktop.docker.com/mac/main/amd64/Docker.dmg?utm_source=docker&utm_medium=webreferral&utm_campaign=docs-driven-download-mac-amd64

### Installation de Docker sous MacOS (*Processeur: ARM*)
Vous pouvez suivre le tutoriel suivant: https://docs.docker.com/desktop/install/mac-install/<br/>
Suite à cela, vous devez exécuter la commande suivante dans votre terminal: `softwareupdate --install-rosetta` <br/>
Et vous pouvez télécharger et installer 'Docker Desktop': https://desktop.docker.com/mac/main/arm64/Docker.dmg?utm_source=docker&utm_medium=webreferral&utm_campaign=docs-driven-download-mac-arm64

### Installation de Docker sous Linux
Vous pouvez suivre le tutoriel suivant: https://docs.docker.com/desktop/install/linux-install/ <br/>

Suite à votre installation de Docker, vous pouvez cloner le dépôt et suivre la prochaine étape.

<br/>

## 3/ Executer les containers & Docker :
Docker est une plateforme de virtualisation légère qui permet de créer, déployer et exécuter des applications dans des conteneurs logiciels. Elle permet ainsi de faciliter la gestion et la portabilité des applications, en isolant leurs dépendances et en assurant une compatibilité entre différents environnements d'exécution.

<br/>

### Commandes utiles

Pour comprendre comment fonctionne Docker, il faut connaître les commandes essentielles qui sont les suivantes :<br/>

`docker ps`: Permet de connaitre les containers en cours d'exécution<br/>
`docker exec -it <ID_CONTAINER> bash`: Permet de rentrer dans le terminal d'un container<br/>
`docker compose build`: Permet de build le dossier courant<br/>
`docker compose up -d`: Permet d'exécuter tous les containers du dossier courant<br/>
`docker compose stop`: Permet d'arrêter tous les containers

<br/><br/>

### Instructions

Ensuite vous pouvez suivre les instructions suivantes pour exécuter vos container docker pour la première fois pour cette SAE.

`cd /path/to/folder/`<br/>
`docker compose build`<br/>
`docker compose up -d`<br/>
Vous pouvez alors ouvrir votre navigateur et allez sur le lien suivant `https://localhost:8082/`, vous pouvez alors voir le site internet.

<br/>

## 5/ PostgreSQL & Postgis
Maintenant que votre serveur Apache est fonctionnel il vous faut que vous installiez votre serveur de base de données sur le container postgres !

<br/>

### Connexion à PostgreSQL

#### PGAdmin
Vous pouvez utiliser PGAdmin, un conteneur a déjà été mis en place pour permettre l'accès à PGAdmin. <br/>
Pour cela, ouvrez votre navigateur et allez à l'adresse `127.0.0.1:5050`. <br/>
Une fois sur l'interface de PGAdmin, vous devez ajouter un serveur. Cependant, vous devez récupérer **l'adresse IP** de votre conteneur. Pour récupérer l'adresse, vous devez faire : <br/>
`docker ps` *Puis récupere l'identifiant du container PostgreSQL* <br/>
`docker inspect <IDENTIFIANT_CONTAINER_POSTGRES>` *Et récupérer l'adresse IP (`IPAddress`)* <br/><br/>

Une fois que vous avez votre adresse IP du container, ouvre PGAdmin puis `Ajouter un nouveau serveur` <br/>
Ajouter un nom, puis allez dans `Connection` <br/>
Dans `Host name/address` mettez l'addresse IP que vous avez récupérer plus tôt <br/>
Enfin dans `Username` et `Password` mettez vos identifiant de connection à PostgreSQL <br/>
Voila vous êtes sur l'interface administrateur de PostgreSQL <br/>
(*PS: Les identifiants de base de PostgreSQL sont `postgres:changeme` *)

<br/>

#### DBeaver et Datagrip
Pour la connexion à PostgreSQL, vous devez ouvrir DBeaver ou Datagrip et rentrer les identifiants de connexion suivants:

```
Host: 127.0.0.1
Port: 5432
User: postgres
Password: postgres
Database: postgres
```

<br/><br/><br/>

Fait par Romain MILLAN et Geoffrey PIERRE
