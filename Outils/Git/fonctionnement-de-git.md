# Fonctionnement de Git

## Concept
__workspace__ est le dossier qui contient votre projet.

__index__ est la base de donnée du __workspace__ qui liste les fichier

__local repository__ et le dépot sur votre ordinateur, qui va contenir 
toutes les modifications locales et celle récupérées sur un autre dépot

__remote repository__ est un autre dépot distant, par exemple github ou votre serveur

Vous pouvez utiser GIT pour versionner des fichiers locaux sur le __local repository__,
sans forcément avoir de dépot distant. Cà peut etre très pratique si vous n'avez pas de
connexion internet. Vous pourrez toujours lier le dépot plus tard, et même le modifier.


## Initalisation et Premiers Commit
### Premier Commit
Pour initialiser son __workspace__ utilisez :

```shell
$ git init
```

Creez un fichier README.md

Ensuite nous allons ajouter ce fichier dans l'index :

```shell
$ git add README.md
```

Et on Versionne tous le fichier ajouté, ce qui aurat pour effet de l'enregistrer dans notre _local respository_:

```shell
$ git commit -m 'Creation ReadMe'
```

Vous pouvez avoir plus d'information en utilisant la commande status

```shell
$ git status
```

### Deuxieme commit

Modifiez le fichier README.md

Si vous faites un _git commit_, il vous dira que le fichier README.md à des modifications non validées,
il faut refaire un _git add_ :

```shell
$ git add README.md
$ git commit -m 'Modification ReadMe 1'
```

### Commiter automatiquement

On viens de voir que le commit ne prenais en compte que les fichiers validés, mais il existe une solution simple
pour commiter tous les fichiers qui ont déjà été indexé :

```shell
$ git commit -am 'Modification ReadMe 2'
```

## Navigation dans l'historique

### Revenir sur une autre version

Pour voir la liste des révision disponible sur le __local repository__, nous utilisons la commande _git log_

```shell
$ git log
```

Nous allons maintenant revenir à la version 1 avec _git checkout &lt;revision&gt;_:

```shell
$ git checkout 28bb2d236ac40649ec921151a087d931ae31bdc2
```

Cette commande permet de voir les fichier, tels qu'ils étaient précédament, pour vraiment revenir en arrier, 
nous allons utliliser la command reset

Vous pouvez préciser un fichier en particulier

```shell
$ git checkout 28bb2d236ac40649ec921151a087d931ae31bdc2 README.md
```

Si vous souhaitez revenir à la version de l'index, cest à dire au dernier commit _Modification Readme 2_,
préciser le nom de la branche, en l'occurence _master_ :

```shell
$ git checkout master
```

Pour revenir définitvement à la version _Modification Readme 1 utilisez _git reset &lt;revision&gt;_ 

```shell
$ git reset 28bb2d236ac40649ec921151a087d931ae31bdc2
$ git commit -am 'Retour version 1'
```

Vous pouvez voir dans l'historique, que les modifications sont définitivemet supprimées :

```shell
$ git log
```

## Intéragir avec un dépot Distant (github)

### Envoyez les modifications
Pour lier le dépot avec github, commencez par creer un "new repository", puis tapez la commande _git remote add origin &lt;url&gt;_ 

```shell
git remote add origin https://github.com/jmaumene/test.git
```

Vous pouvez maintenant envoyez vos modifications sur le __remote repository__ avec la commande _git push -u &lt;branche&gt;_

```shell
$ git push -u origin master
```

Si vous vous connectez sur github, et que vous regarer l'historique du fichier, vous retrouverez toutes les modifications, 
jusqu'au retour à la version 1.

### récuperer toutes les modifications

Nous pouvons soit mettre à jours notre __local repository__, avec la commande fetch
```shell

$ git fetch
```
puis on merge :

```shell
$ git merge
```


Soit récuperer directement les modification dans notre __workspace__ avec la commande _pull__ 
( qui correspond à _fetch_ + _merge_ )

```shell
$ git pull
```


