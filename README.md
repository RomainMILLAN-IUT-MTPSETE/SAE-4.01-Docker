# Docker - TP2
Ce dépôt à était crée pour le TP 2 du cours de Virtualisation.<br/>
Dépôt crée par Romain MILLAN et Geoffrey PIERRE

<br/>

## Pour répondre au TP

### Docker Compose & Dockerfile
#### Docker Compose
Dans le docker compose nous avons mis en place 3 container différents qui se nomment <br/>
- 'rmgp_apache': Serveur apache<br/>
- 'rmgp_postgres': Serveur postgres<br/>
- 'rmgp_pgadmin': Serveur pgadmin<br/>
<br/>

Dans le container 'rmgp_apache' et 'rmgp_postgres' nous avons utilisée des Dockerfile pour crée les container au contraire du container 'rmgp_pgadmin' nous avons utiliser directement l'image `dpage/pgadmin4`.
<br/>

##### rmgp_apache
```Docker
build: docker/apache //Utilise le fichier Dockerfile contenue dans le dossier docker/apache
container_name: rmgp_apache //Nom du container
volumes: //Liste les volumes
 - ./web_rmgp:/var/www/html:cached //Redirige le dossier 'web_rmgp' vers '/var/www/html'
 - ./docker/apache/sites_enabled:/etc/apache2/sites_enabled //Fichier config
 - ./docker/php/custom-php.ini:/use/local/etc/php/conf.d/custom-php.ini //Fichier config
environment: //Données environement
    max_execution_time: 2000
depends_on: //Veut dire que le container dépend du container 'postgres'
 - postgres
ports: //Initialise le port
 - "8082:80" //Le port 80 redirection vers 8082
```

##### rmgp_postgres
```
build: docker/postgres //Utilise le fichier Dockerfile contenue dans le dossier docker/postgres
container_name: rmgp_postgres //Nom du container
environment: //Données environement
    POSTGRES_USER: ${POSTGRES_USER:-postgres}
    POSTGRES_PASSWORD: ${POSTGRES_PASSWORD:-postgres}
    PGDATA: /data/postgres
volumes: //Liste les volumes
    - postgres:/data/postgres //Les données de postgres viendrons directement dans postgres
ports: //Initialise le port
    - "5432:5432" //Port 5432 vers 5432
networks: //Met le container dans le network nomée 'postgres'
    - postgres
restart: unless-stopped //Restart dès que le container crash
```

##### rmgp_pgadmin
```
container_name: rmgp_pgadmin //Nom du container
image: dpage/pgadmin4 //Image utiliser pour le container ici 'dpage/pgadmin4'
environment: //Données environement
    PGADMIN_DEFAULT_EMAIL: ${PGADMIN_DEFAULT_EMAIL:-pgadmin4@pgadmin.org}
    PGADMIN_DEFAULT_PASSWORD: ${PGADMIN_DEFAULT_PASSWORD:-admin}
    PGADMIN_CONFIG_SERVER_MODE: 'False'
volumes: //Liste les volumes
    - ./pgadmin:/var/lib/pgadmin
ports: //Initialise le port
    - "${PGADMIN_PORT:-5050}:80" //Port 80 vers port 5050
networks: //Met le container dans le network nomée 'postgres'
    - postgres
restart: unless-stopped //Restart dès que le container crash
```

##### networks
```
networks:
  postgres:
    driver: bridge
```
Crée un network nomée postgres avec le driver bridge.<br/>

<br/>

### Build et Run des containers
Pour éxécuter le tp il vous suffit d'utiliser les commandes suivantes: <br/>
- `docker compose build`<br/>
- `docker compose up -d`<br/>

<br/>

Vous pouvez donc constater que les 3 container (Apache, PostgreSQL avec Postgis, PGAdmin) sont lancée. Vous pouvez consulter le résultat avec la commande:<br/>
- `docker ps`<br/>

<br/>

Vous pouvez vous rendre sur le site http://localhost:8082/ pour consulter le résultat.

<br/>
<br/>
Crée par Romain MILLAN et Pierre GEOFFREY.

<br/>
<br/>
<br/>

# Pour compléter

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
