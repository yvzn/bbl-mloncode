# bbl-mloncode
12@13 Machine Learning on Code (restitution Devfest Nantes 2019)

La présentation se trouve dans le fichier presentation.markdown

Elle peut être visualisée [sur Github pages](https://yvzn.github.io/bbl-mloncode)

## Setup

L'affichage des slides utilise le framework de présentation
[RevealJS](https://revealjs.com/)
ajouté en tant que submodule git au projet.

Pour récupérer le code source

```bash
$ git clone --recurse-submodules https://github.com/yvzn/bbl-mloncode.git
$ cd bbl-mloncode
```

## Démarrage

Pour lancer le serveur (par exemple avec NodeJS)

```bash
$ npx http-server -p 8080
```

Autre solution (avec Python)

```bash
$ python -m http.server 8080
```

Puis ouvrir <http://127.0.0.1:8080/?showNotes=separate-page> dans le navigateur

Ou pour la version imprimable <http://127.0.0.1:8080/?print-pdf&showNotes=separate-page>

## Licensing

Le texte de cette présentation est sous licence MIT.

Cette présentation utilise:
* du code source libre sous licence MIT (RevealJS) ou BSD (Highlight.js)
* des polices sous licence OFL (Lato)
