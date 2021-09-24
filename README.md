# Web-server

- Objectif : Faire le meilleur serveur de fichiers HTTP.
- Caractéristiques : interface utilisateur conviviale, prise en charge du téléchargement de fichiers.

**Sources** disponibles [sur le dépôt officiel](https://github.com/codeskyblue/gohttpserver/)

## Fonctionnalités
1. [x] Modification rapide du chemin du fil d'Ariane
1. [x] Package de tous les actifs en binaire autonome
1. [x] Icône différente en fonction du type de fichier
1. [x] Possibilité d'afficher ou masquer les fichiers cachés
1. [x] Mise en place de téléchargement
1. [x] Rechargement partiel des pages lors d'un changement de répertoire
1. [x] Lorsqu'un seul dossier sous-dossier, le chemin en combinera deux
1. [x] Téléchargement du répertoire zip
1. [x] CORS activé
1. [x] Recherche globale de fichiers
1. [x] Ajouter des informations de version dans la page d'index
1. [x] Version de balise automatique
1. [x] Prise en charge des titres personnalisés
1. [x] Paramètres de prise en charge du fichier de configuration
1. [x] Lien de téléchargement rapide
1. [x] Afficher la taille du dossier
1. [x] Créer un dossier
1. [x] Ignorer la suppression et confirmer lorsque vous appuyez sur alt
1. [x] Prend en charge la décompression du fichier zip lors du téléchargement (avec le formulaire : unzip=true)
1. [ ] Calculer md5 et sha
1. [ ] Aperçu du fichier de code
1. [ ] Téléchargement de dossier

## Usage
Configurer le fichier de configuration **config.yml** (la liste des arguments est diponible grâce à la commande `gohttpserver --help`) :

```
upload: true
delete: true
title: "Partage BCS"
root: "/tmp/test/"
```

Le paramètre *upload* permet d'autoriser le téléversement de fichier".\
Le paramètre *delete* permet d'autoriser la suppression de fichier et de dossier.\
Le paramètre *title* permet de personnaliser le titre qui s'affiche sur la page web.\
Le paramètre *root* permet de spécifier le dossier racine du partage de fichier.\

Avant de lancer le serveur, veillez à ce que le fichier configuration soit dans le même dossier que le script **gohttpserver** puis faites la commande suivante :

```
./gohttpserver --conf=config.yml
```

### Téléverser avec CURL
Par exemple, téléverser un fichier `foo.txt` dans le dossier `somedir` :

```sh
$ curl -F file=@foo.txt localhost:8000/somedir
{"destination":"somedir/foo.txt","success":true}

# upload and change filename
$ curl -F file=@foo.txt -F filename=hi.txt localhost:8000/somedir
{"destination":"somedir/hi.txt","success":true}
```

Téléverser un fichier zip et décompresser le :

```sh
$ curl -F file=@pkg.zip -F unzip=true localhost:8000/somedir
{"success": true}
```

Note: `\/:*<>|` ne sont pas autorisé dans le nom des fichiers.

## FAQ
### Comment les requêtes sont formées
Les recherches suivent des règles de format communes, tout comme Google. Les mots-clés sont séparés par des espaces, les mots-clés avec préfixe "-" seront exclus des résultats de recherche.

1. `hello world` doit contenir `hello` et `world`
1. `hello -world` doit contenir `hello` mais ne doit pas contenir `world`

### Comment on met le script à jour ?
Pourquoi on le ferait ? Ca fonctionne bien...

### Comment on modifie le script ?
1. Apprendre à coder en golang (https://golang.org/)
1. Télécharger les sources (https://github.com/codeskyblue/gohttpserver/)
1. Faire les modifications grâce à votre éditeur de texte favori
1. Installer Golang (https://golang.org/dl/)
1. Faire la commande `go build` pour le compiler sous linux.
1. Fin !

## Développement et compilation

1. Construire la version de développement. Le répertoire **assets** doit exister

  ```sh
  go build
  ```
2. Construire une seule version binaire

  ```sh
  go generate .
  go build -tags vfs
  ```

Les thèmes sont définis dans le répertoire [assets/themes](assets/themes). Désormais, seuls deux thèmes sont disponibles, "noir" et "vert".

## Références

* Core lib Vue <https://vuejs.org.cn/>
* Icon from <http://www.easyicon.net/558394-file_explorer_icon.html>
* Code Highlight <https://craig.is/making/rainbows>
* Markdown Parser <https://github.com/showdownjs/showdown>
* Markdown CSS <https://github.com/sindresorhus/github-markdown-css>
* Upload support <http://www.dropzonejs.com/>
* ScrollUp <https://markgoodyear.com/2013/01/scrollup-jquery-plugin/>
* Clipboard <https://clipboardjs.com/>
* Underscore <http://underscorejs.org/>

**Go Libraries**

* [vfsgen](https://github.com/shurcooL/vfsgen)
* [go-bindata-assetfs](https://github.com/elazarl/go-bindata-assetfs)
* <http://www.gorillatoolkit.org/pkg/handlers>

## LICENCE
Ce projet est sous licence MIT (enfin, les sources du Github d'origine).
