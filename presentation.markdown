
# ML on Code
Devfest Nantes 2019

note:
* machine learning
* sur son source code 
* retour sur le Codelab 

---

## source{d}
* Alex Bezzubov <!-- .element: class="fragment" -->
* Hugo Mougard <!-- .element: class="fragment" -->

note:
* speakers
* éditeur, data & analytics

---

<!-- .slide: data-background-image="resources/IMG_20191021_163223.jpeg" class="dark-bg" -->

---

## liens
* [GitHub codelab](https://github.com/mloncode/devfest2019-workshop) 
* [Slides codelab](https://docs.google.com/presentation/d/1vF0JMagmXXzn-h-OaJu6CsDt78oSQSg58YFJsBUaHxk/edit)
* [Slides présentation MLonCode](https://egorbu.github.io/usedata_2019/) 

---

<iframe width="1120" height="630" src="https://www.youtube.com/embed/6NhQIaJfWXk" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

note:
* domaine récent (2-3 ans)
* beaucoup de publications récentes (MS, Google, FB)
* conférences

---

## Objectifs
* comprendre son code <!-- .element: class="fragment" -->
* améliorer l'outillage <!-- .element: class="fragment" -->

note:
* extraire des métriques
* identifier des (anti-)patterns
* "IntelliCode" (auto-complétion contextuelle, refactoring, ...)

---

## Approches
* syntaxe "naturelle" du code <!-- .element: class="fragment" -->
* Natural Language Processing <!-- .element: class="fragment" -->

note:
* plusieurs approches possibles
* considérer que la formulation du code "imite" le langage naturel (LN)
  * identifiants, liens logiques (if, for, etc.)
  * une hypothèse forte / un a priori fort
* permet d'utiliser les patterns statistiques déjà connus en (LN)
* a ses limites (structure du code)

---

## Etapes
1. Problem statement <!-- .element: class="fragment" -->
1. Data collection <!-- .element: class="fragment" -->
1. Exploration <!-- .element: class="fragment" -->
1. Evaluation <!-- .element: class="fragment" -->
1. Communication <!-- .element: class="fragment" -->

note:
* projet de data science
* tâches classiques

---

## Le codelab
* détecter des projets similaires <!-- .element: class="fragment" -->
* nommer une méthode via son contenu <!-- .element: class="fragment" -->

note:
* regroupements par thème (sécurité...)

---

## Collecter la donnée
* liste d'organisations Github <!-- .element: class="fragment" -->
* liste de repos <!-- .element: class="fragment" -->
* API Github <!-- .element: class="fragment" -->

note:
* donnée = code source
* peut sembler trivial ? problématiques de performance et de stockage
* eviter les gros repos / seulement repos avec x stars
* exemple d'organisation intéressante: Apache

---

## Collecter la donnée
* `git clone` / `git checkout` <!-- .element: class="fragment" -->
* filtrage / nettoyage <!-- .element: class="fragment" -->

note:
* performances réseau (paralléliser)
* nettoyer
  * vendor directories
  * configs protobuf ...

---

## Gitbase

![modèle de données Gitbase](https://raw.githubusercontent.com/src-d/gitbase/master/docs/assets/gitbase-schema.png)

note:
* expose les repos comme une base de données
* simplifier l'exploration via SQL
* outil développé par source{d}

---

## Gitbase

![modèle de données simplifié Gitbase](https://raw.githubusercontent.com/mloncode/devfest2019-workshop/master/notebooks/img/tables.png)

note:
* tables utilisées pour le codelab
* blob_content = code source
* plus rapide que de parser les fichiers du '.git'

---

## Gitbase
* https://github.com/src-d/gitbase

---

## Analyser la donnée
* comme un flux des caractères ? <!-- .element: class="fragment" -->
* parser les fichiers ? <!-- .element: class="fragment" -->
* pour chaque langage ? <!-- .element: class="fragment" -->

---

## Babelfish
![capture d'écran Babelfish](resources/babelfish.png)

note:
* outil permettant de construire un arbre syntaxique
* a partir d'un fichier source

---

## Babelfish
* Abstract Syntax Tree (AST) <!-- .element: class="fragment" -->
* 15+ langages <!-- .element: class="fragment" -->

---

## Babelfish
* Requêtable via XPath <!-- .element: class="fragment" -->
* Requêtable via Gitbase <!-- .element: class="fragment" -->

note:
* facilité de mise en oeuvre
* plus rapide que boucles / parsing / regexp à la main
---

## Babelfish
* https://doc.bblf.sh/

---

## Similarité entre projets
* utiliser les identifiants pour analyser les projets <!-- .element: class="fragment" -->
* apprentissage non supervisé <!-- .element: class="fragment" -->

---

## Extraire les identifiants
* décomposition (`tcp_socket_connect` ➡ `[tcp, socket, connect]`) <!-- .element: class="fragment" -->
* filtrer <!-- .element: class="fragment" -->

note:
* décomposer pour réduire le vocabulaire
  * russian 150k, japanese 500K, ..., dev identifiers 49M
  * enlever les identifiants rares / pas les stop words
* Gitbase + babelfish

---

## Topic Modeling
* identifiants qui apparaissent souvent ensemble <!-- .element: class="fragment" -->
* définit un topic <!-- .element: class="fragment" -->
* non supervisé <!-- .element: class="fragment" -->

note:
* notion abstraite pour la machine 
* pas de "signification" des topics (topic_1, topic_2, ...) 

---

## Topic Modeling
![Topics vs identifiants (extrait)](resources/topics_vs_identifiers.png)

---

## BigARTM
* http://bigartm.org/

note:
* outil pour construire les topics en analysant le code source
* définir le nombre de topics souhaités

---

## Topic Modeling
* sparsing <!-- .element: class="fragment" -->
* moyenner <!-- .element: class="fragment" -->
* `git blame` <!-- .element: class="fragment" -->
* comparer <!-- .element: class="fragment" -->

note:
* sparsing
  * supprimer (mettre à 0) les topics avec des scores faibles
  * plus simple à interpréter
* pour tous les fichiers d'un même repo
* topics du repo
* comparaison abstraite repo/repo - repo/dev - dev/dev

---

## Visualiser
![Topics via pyLDAvis](resources/pyldaviz.png)

---

## pyLDAvis
* https://github.com/bmabey/pyLDAvis

note:
* visualiser les topics générés par BigARTM

---

## Nommer une méthode

note:
* modèles de traduction automatisée
* OpenNMT / seq2seq
* pas pu être abordé par manque de temps

---

## Conclusion
* ML on code <!-- .element: class="fragment" -->
* approche NLP <!-- .element: class="fragment" -->
* taches simples <!-- .element: class="fragment" -->

note:
* IntelliCode
* auto-complétion en fonction du contexte
* repérer les erreurs difficiles à identifier
* (anti-)patterns / code stytle

---

## Conclusion
* Etapes d'un projet de data science <!-- .element: class="fragment" -->
* Outils pour se faciliter la tâche <!-- .element: class="fragment" -->

note:
* la majorité du travail = collecter / nettoyer la data

---

<!-- .slide: data-background-image="resources/IMG_20191021_164404.jpeg" class="dark-bg" -->

