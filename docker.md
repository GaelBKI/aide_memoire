# Commandes Docker

## Créer et lancer un conteneur

```bash
docker run <nom de l\'image>
```

## Créer, lancer et nommer un conteneur

```bash
docker run --name=<nom du conteneur> <nom de l\'image>
```

## Lister les conteneurs

```bash
docker ps
```

```bash
docker container ps
```

### Lister tous les conteneurs

```bash
docker ps -a
```

```bash
docker container ps -a
```

## Lister les images

```bash
docker image ls
```

```bash
docker images
```

## Supprimer un ou plusieurs conteneurs

```bash
docker rm <id du conteneur>
```

```bash
docker container rm <id du conteneur>
```

## Supprimer une ou plusieurs images

```bash
docker image rm <id de l\'image>
```

```bash
docker rmi <id de l\'image>
```

## Lancer un conteneur et intéragir

```bash
docker run -it <nom de l\'image>
```

## Lancer un conteneur et le supprimer automatiquement

```bash
docker run -it --rm <nom de l\'image>
```

## Redémarrer un conteneur

```bash
docker start <id du conteneur>
```

## Arrêter un conteneur

```bash
docker stop <id du conteneur>
```

## Entrer et intéragir dans un conteneur déjà démarré

```bash
docker exec -it <id du conteneur> bash
```

## Redémarrer et intéragir avec un conteneur en une ligne de commande

```bash
docker start -ai <id du conteneur>
```

## Volumes

### Mappé

```bash
docker run -it -v <chemin complet dossier local>:<chemin complet dossier conteneur> <nom de l\image>
```

### Managé

#### Créer un volume

```bash
docker volume create <nom du volume>
```

#### Lister les volumes

```bash
docker volume ls
```

#### Supprimer un volume

```bash
docker volume rm <nom du volume>
```

#### Lier un volume

```bash
docker run -it <nom du volume>:<chemin complet dossier conteneur> <nom de l\'image>
```

#### Information du volume

```bash
docker volume inspect <nom du volume>
```
## Télécharger une image

```bash
docker pull <nom de l\'image>:<version de l\'image>
```

## Réseau

### Mapper un port

```bash
docker run -p <port local>:<port conteneur> <nom de l'\image>
```

### Lister les réseaux

```bash
docker network ls
```

### Créer un réseau docker

```bash
docker network create --driver=<driver réseau à utiliser> <nom du réseau>
```

### Démarrer un conteneur avec un réseau spécifique

```bash
docker run --network=<nom du réseau docker> <nom de l'\image>
```

### Isoler un conteneur

```bash
docker run --network=none <id de l'\image>
```

### Connecter un conteneur avec un réseau spécifique

```bash
docker network connect <nom du réseau docker> <nom du conteneur>
```

### Déconnecter un conteneur d'un réseau

```bash
docker network disconnect <nom du réseau docker> <nom du conteneur>
```

### Vérifier les conteneurs présents dans un réseau

```bash
docker network inspect <nom du réseau docker>
```

### Supprimer un réseau

```bash
docker network rm <nom du réseau docker>
```

## Dockerfile

### Exemple de Dockerfile (fichier nommé Dockerfile sans extension)

```bash
FROM <nom de l\'image source>:<version de l\'image source>
WORKDIR <dossier de travail dans le conteneur>
COPY <chemin vers le fichier à copier> <chemin du dossier dans le conteneur (depuis WORKDIR)>
RUN <commande1>
RUN <commande2>
CMD ["<nom du programme à lancer au démarrager du conteneur", "<parametre 1>","<parametre 2>"]
```

### Construire une image personnalisée

```bash
docker build -t <nom de l\'image personnalisée> <chemin du fichier Dockerfile>
```

### Ajouter une image personnalisée sur Dockerhub

```bash
docker tag <nom de l\'image locale> <nom du repository dockerhub>
docker push <nom du repository dockerhub>
```

## Docker-compose

Être positionné dans le répertoire contenant le fichier docker-compose.yml

### docker-compose.yml simple

```docker
services:
    <nom du service>:
        image: <image de base>
        container_name: <nom du conteneur>
```

### Démarrer le docker-compose.yml

```bash
docker compose up
```

Démarrer le docker-compose.yml en mode daemon (arrière plan)

```bash
docker compose up -d
```

### Intéragir avec le conteneur

```docker
services:
    <nom du service>:
        image: <image de base>
        container_name: <nom du conteneur>
        stdin_open: true
        tty: true
```

Ensuite utiliser la commande suivante :

```bash
docker exec -it <id ou nom du conteneur> bash
```

### Arrêter un ou plusieurs conteneurs

```bash
docker compose stop
```

### Supprimer un ou plusieurs conteneurs

```bash
docker compose rm
```

### Volume mappé

```docker
services:
    <nom du service>:
        image: <image de base>
        container_name: <nom du conteneur>
        stdin_open: true
        tty: true
        volumes:
            - <chemin du dossier local>:<chemin du dossier dans le conteneur>
```

### Volume managé

```docker
services:
    <nom du service>:
        image: <image de base>
        container_name: <nom du conteneur>
        stdin_open: true
        tty: true
        volumes:
            - <nom_du_volume>:<chemin dans le conteneur>
volumes:
    <nom_du_volume>:
```

### Réseau

Tous les conteneurs du docker-compose.yml sont automatiquement connecté à un réseau.

#### Réseau personnalisé

```docker
services:
    <nom du service 1>:
        image: <image de base>
        container_name: <nom du conteneur 2>
        stdin_open: true
        tty: true
        networks:
            - <nom du reseau 1>

    <nom du service 2>:
        image: <image de base>
        container_name: <nom du conteneur 2>
        stdin_open: true
        tty: true
        networks:
            - <nom du reseau 1>
networks:
    <nom du réseau 1>:
        driver: <type du réseau>
```

### Port redirigé

```docker
services:
    <nom du service>:
        image: <image de base>
        container_name: <nom du conteneur>
        ports:
            - "<port local>":"<port dans le conteneur>"
```

### Construire une image personnalisée

```docker
services:
    <nom du service>:
        build: <emplacement du fichier Dockerfile>
        container_name: <nom du conteneur>
```

Lancer docker compose avec le paramètre --build

```bash
docker compose up --build
```
