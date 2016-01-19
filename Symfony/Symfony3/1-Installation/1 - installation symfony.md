# Installation de symfony, paramétrage et création de projet

## Installation de symfony

```shell
$ sudo curl -LsS https://symfony.com/installer -o /usr/local/bin/symfony
$ sudo chmod a+x /usr/local/bin/symfony
```

## Paramétrage de apache

Modifier le timezone, qui n'est pas défini par défaut
```
# php.ini
date.timezone = Europe/Paris
```

## Création du projet
```shell
$ symfony new my_project_name
```

Possibilité de préciser la version, ou lts :
```shell
$ symfony new my_project_name lts
$ cd my_project_name
$ composer install
```

## Lancement project

```shell
$ cd my_project_name/
$ php bin/console server:run
```

Se connecter sur http://localhost:8000/config.php et si tout est bon votre projet peut etre visible ici http://localhost:8000/

## Permissions

```shell
$ sudo setfacl -R -m u:"www-data":rwX -m u:`whoami`:rwX var
$ sudo setfacl -dR -m u:"www-data":rwX -m u:`whoami`:rwX var
```