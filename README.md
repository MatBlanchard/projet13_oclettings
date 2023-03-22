## Résumé

Site web d'Orange County Lettings

## Développement local

### Prérequis

- Compte GitHub avec accès en lecture à ce repository
- Git CLI
- SQLite3 CLI
- Interpréteur Python, version 3.6 ou supérieure

Dans le reste de la documentation sur le développement local, il est supposé que la commande `python` de votre OS shell exécute l'interpréteur Python ci-dessus (à moins qu'un environnement virtuel ne soit activé).

### macOS / Linux

#### Cloner le repository

- `cd /path/to/put/project/in`
- `git clone https://github.com/OpenClassrooms-Student-Center/Python-OC-Lettings-FR.git`

#### Créer l'environnement virtuel

- `cd /path/to/Python-OC-Lettings-FR`
- `python -m venv venv`
- `apt-get install python3-venv` (Si l'étape précédente comporte des erreurs avec un paquet non trouvé sur Ubuntu)
- Activer l'environnement `source venv/bin/activate`
- Confirmer que la commande `python` exécute l'interpréteur Python dans l'environnement virtuel
`which python`
- Confirmer que la version de l'interpréteur Python est la version 3.6 ou supérieure `python --version`
- Confirmer que la commande `pip` exécute l'exécutable pip dans l'environnement virtuel, `which pip`
- Pour désactiver l'environnement, `deactivate`

#### Exécuter le site

- `cd /path/to/Python-OC-Lettings-FR`
- `source venv/bin/activate`
- `pip install --requirement requirements.txt`
- `python manage.py runserver`
- Aller sur `http://localhost:8000` dans un navigateur.
- Confirmer que le site fonctionne et qu'il est possible de naviguer (vous devriez voir plusieurs profils et locations).

#### Linting

- `cd /path/to/Python-OC-Lettings-FR`
- `source venv/bin/activate`
- `flake8`

#### Tests unitaires

- `cd /path/to/Python-OC-Lettings-FR`
- `source venv/bin/activate`
- `pytest`

#### Base de données

- `cd /path/to/Python-OC-Lettings-FR`
- Ouvrir une session shell `sqlite3`
- Se connecter à la base de données `.open oc-lettings-site.sqlite3`
- Afficher les tables dans la base de données `.tables`
- Afficher les colonnes dans le tableau des profils, `pragma table_info(Python-OC-Lettings-FR_profile);`
- Lancer une requête sur la table des profils, `select user_id, favorite_city from
  Python-OC-Lettings-FR_profile where favorite_city like 'B%';`
- `.quit` pour quitter

#### Panel d'administration

- Aller sur `http://localhost:8000/admin`
- Connectez-vous avec l'utilisateur `admin`, mot de passe `Abc1234!`

### Windows

Utilisation de PowerShell, comme ci-dessus sauf :

- Pour activer l'environnement virtuel, `.\venv\Scripts\Activate.ps1` 
- Remplacer `which <my-command>` par `(Get-Command <my-command>).Path`

## Déploiement

#### Prérequis

- Avoir le code est sur votre propre depot GitHub. (le nom du depot github doit absolument être en minuscule)
- Avoir créé un compte sur DockerHub.
- Avoir créé un compte sur Heroku.

#### Docker

Clonez le repository en local et entrez les commandes suivantes à l'endroit du depot local : 

- `docker build -t <your-app-name> .`
- `docker tag <your-app-name>:latest <your-docker-username>/<your-app-name>:latest`
- `docker push <your-docker-username>/<your-app-name>:latest`

#### CircleCi

Connectez-vous à CircleCi en utilisant GitHub.

Dans la section "Set up a project", sélectionnez le depot GitHub du projet et utilisez l'option "Fastest".

Dans la section "Project", cliquez sur les 3 petits points à côté du bouton "Unfollow Project" 
et sélectionnez "Project Settings".

Dans la section "Environment Variables" créer les variables suivantes :
- DOCKER_PASSWORD (votre mot de passe Docker)
- DOCKER_USERNAME (votre nom d'utilisateur Docker)
- HEROKU_API_KEY (trouvable dans la section "Account settings" sur heroku)
- HEROKU_APP_NAME (le nom de l'application sur Heroku)

Enfin, vous n'avez qu'à faire un push sur la branche main du GitHub pour déclencher le déploiement.
Celui-ci se déclenchera uniquement si CircleCi ne détecte pas d'erreurs durant la compilation, les tests ou 
la conteneurisation de l'application.

Le processus de déploiement via CircleCi prend 2 à 3 min, vous pouvez suivre l'avancée de celui-ci sur 
la section "Dashboard" de CircleCi

:warning: Heroku est devenu payant depuis novembre 2022, le déploiement du site vous coutera 7$/mois. 
Il faut donc entrer un moyen de paiement sur votre compte Heroku ! :warning:

#### Sentry

Une fois le déploiement effectué, vous pourrez suivre les erreurs de celle-ci de la façon suivante :

- Allez dans la section "Dashboard" de Heroku.
- Cliquez sur l'application que vous venez de déployer.
- Dans la section "Installed add-ons", cliquez sur Sentry.


