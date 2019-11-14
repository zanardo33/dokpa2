# MariaDB

## Introduction
Voici mon conteneur Mariadb, c'est un conteneur qui permet d'illustrer l'utilisation de Docker.

## Fonctionnement
Ce conteneur est basé sur Alpine Linux version 3.10 afin d'obtenir un conteneur minimal. 
Il s'agit d'une installation standard de MariaDb.
Lors du lancement du conteneur, le script *launch* est lancé via la commande CMD du Dockerfile. Cette commande peut en conséquence être neutralisée en lancant directement une autre commande.

### Launch (/usr/local/bin/launch)
Lors du lancement du script, le système vérifie la présence de la base *test* dans l'aborescence /var/lib/mysql. 
Si cette base n'est pas trouvée, cela signifie que le volume contient déjà une base, le script lance le serveur mysqld avec exec (afin de transmettre le kill -TERM) lors de l'arrêt du conteneur.

Si la base n'est pas trouvée, alors le script crée une base et un compte associé grâce aux variables d'environnement passées:
* **MYSQL_ROOT_PASSWORD**    mot de passe root pour MariaDB
* **MYSQL_DATABASE**         nom de la base à créer
* **MYSQL_USER**             nom de l'utilisateur
* **MYSQL_PASSWORD**         mot de passe associé
Puis lance le serveur.

## Utilisation

Lors du premier lancement, penser à initialiser les variables:
> docker run -d -e MYSQL_ROOT_PASSWORD='secret' -e MYSQL_DATABASE='database' -e MYSQL_USER='user' -e MYSQL_PASSWORD='secret' -v VolDB:/var/lib/mysql easylinux/mariadb

Les lancements suivants pourront se faire ainsi :
> docker run -d -v VolDB:/var/lib/mysql easylinux/mariadb

Pour lancer le conteneur sans activer le script :
> docker run -it -v VolDB:/var/lib/mysql easylinux/mariadb /bin/sh
  
**NB:** 
* Pour des raisons de sécurité, il est déconseillé de publier le port *3306*, nous vous conseillons plutôt de dédier un réseau.
* Le paquet mariadb-client n'est pas présent dans le conteneur, seul le moteur de la base s'y trouve
