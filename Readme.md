# Lancement initial
Lors du premier lancement sur un projet qui va être initialisé, le but est de copier le dossier `/opt/drupal` du container dans le dossier `www` de l'hôte afin qu'ils puissent être modifiés.

- Immédiatement après le clonage du dépôt, changer le remote pour ne pas écraser le dépôt "Drupal Docker Compose"
- Changer le nom de PROJECT NAME dans le .env (doit respecter [a-zA-Z0-9][a-zA-Z0-9_.-])
- Vérifier que les lignes 12 et 13 sont commentées dans docker-compose.yml
- lancer "docker compose up -d"
- lancer les commandes: \
	docker cp drupal_$PROJECT_NAME:/opt/drupal/. ./www/.
- décommenter les lignes
- détruire le container drupal_$PROJECT_NAME et relancer "docker compose up -d"

Pour faire cohabiter plusieurs environnements similaires, il est possible de changer les numéros de port des services dans le .env pour éviter les collisions.

# Mise à jour des images Docker
Si vous souhaitez mettre à jour une image et si vous avez deja installer ce projet il vous faudra lancer ces différentes commandes :
- docker compose down (dans la racine du projet)
- docker compose build
- docker compose up -d

# Issues
## Timeout Composer

Si vous avez un timeout de composer avec cette erreur :
```
Update of drupal/core failed
The following exception is caused by a process timeout
Check https://getcomposer.org/doc/06-config.md#process-timeout for details

In Process.php line 1204:
  The process "rm -rf 'web/core'" exceeded the timeout of 300 seconds.
```

Il faudra lancer cette commande :  `composer config --global process-timeout 2000`


# Urls d'accées

## Drupal
http://127.0.0.1:9999

## PHPMyAdmin
http://127.0.0.1:10000

## MySQL
Au lancement initial une base de données nommée "drupal" est créée. \
Lors de l'installation de Drupal, l'hôte MySQL qui doit être renseigné est `mysql_$PROJECT_NAME` \
Les identifiants sont root/password (si inchangés dans le .env)
