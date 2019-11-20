
# ML on Code
Devfest Nantes 2019

note:
* machine learning
* on source code 

---

## source{d}
* Alex Bezzubov <!-- .element: class="fragment" -->
* Hugo Mougard <!-- .element: class="fragment" -->

---

## liens
* [GitHub codelab](https://github.com/mloncode/devfest2019-workshop) 
* [Slides codelab](https://docs.google.com/presentation/d/1vF0JMagmXXzn-h-OaJu6CsDt78oSQSg58YFJsBUaHxk/edit)
* [Slides présentation](https://egorbu.github.io/usedata_2019/) 

---

<iframe width="1120" height="630" src="https://www.youtube.com/embed/6NhQIaJfWXk" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

note:
* domaine récent (2-3 ans)
* publications++ (MS, Google, FB)
* conférences

---

## Objectifs
* comprendre son code <!-- .element: class="fragment" -->
* améliorer l'outillage <!-- .element: class="fragment" -->

note:
* extraire des métriques
* IntelliCode


---

## Approches
* syntaxe "naturelle" du code <!-- .element: class="fragment" -->
* Natural Language Processing <!-- .element: class="fragment" -->

note:
* plusieurs approches possibles
* code "imite" le LN
* une approche / hypothèse forte
* patterns statistiques (~LN)
* limites (structure du code)

---

## Etapes
1. Problem statement <!-- .element: class="fragment" -->
1. Data collection <!-- .element: class="fragment" -->
1. Exploration <!-- .element: class="fragment" -->
1. Evaluation <!-- .element: class="fragment" -->
1. Communication <!-- .element: class="fragment" -->

note:
* data science
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
* 1ère étape
* donnée = code source
* trivial ?
* eviter les gros repos / seult repos avec x stars
* exemple: Apache

---

## Collecter la donnée
* `git clone` / `git checkout` <!-- .element: class="fragment" -->
* filtrage / nettoyage <!-- .element: class="fragment" -->

note:
* performance
* vendor directories
* protobuf configs ...

---

## Gitbase

![modèle de données Gitbase](https://raw.githubusercontent.com/src-d/gitbase/master/docs/assets/gitbase-schema.png)

note:
* expose les repos comme une base de données
* simplifier l'exploration via SQL

---

## Gitbase

![modèle de données simplifié Gitbase](https://raw.githubusercontent.com/mloncode/devfest2019-workshop/master/notebooks/img/tables.png)

note:
* blob_content = code source

---

## Gitbase
* https://github.com/src-d/gitbase

---

## Analyser la donnée
* "juste" des caractères ? <!-- .element: class="fragment" -->
* parser les fichiers ? <!-- .element: class="fragment" -->
* pour chaque langage ? <!-- .element: class="fragment" -->

---

## Babelfish
![capture d'écran Babelfish](resources/babelfish.png)

note:
* arbre syntaxique
* a partir d'un fichier source

---

## Babelfish
* Abstract Syntax Tree (AST) <!-- .element: class="fragment" -->
* 15+ langages <!-- .element: class="fragment" -->

---

## Babelfish
* Requêtable en XPath <!-- .element: class="fragment" -->
* Requêtable via Gitbase <!-- .element: class="fragment" -->

note:
* facilité de mise en oeuvre
* vs boucles / parsing / regexp
---

## Babelfish
* https://doc.bblf.sh/

---

## Similarité entre projets
* utiliser les identifiants <!-- .element: class="fragment" -->
* apprentissage non supervisé <!-- .element: class="fragment" -->

---

## Extraire les identifiants
* décomposition (`tcp_socket_connect` ➡ `[tcp, socket, connect]`) <!-- .element: class="fragment" -->
* filtrer <!-- .element: class="fragment" -->

note:
* Gitbase + babelfish
* réduire le vocabulaire
* russian 150k, japanese 500K, ..., dev identifiers 49M
* enlever les identifiants rares / pas les stop words

---

## Topic Modeling
* identifiants qui apparaissent souvent ensemble <!-- .element: class="fragment" -->
* non supervisé <!-- .element: class="fragment" -->

note:
* notion abstraite
* pas de "signification" des topics 

---

## Topic Modeling
![Topics vs identifiants (extrait)](resources/topics_vs_identifiers.png)

---

## BigARTM
* http://bigartm.org/

---

## Topic Modeling
* sparsing <!-- .element: class="fragment" -->
* moyenner <!-- .element: class="fragment" -->
* `git blame` <!-- .element: class="fragment" -->
* comparer <!-- .element: class="fragment" -->

note:
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

---

## Nommer une méthode

note:
* modèles de traduction automatisée
* OpenNMT / seq2seq

---

## Conclusion
* ML on code <!-- .element: class="fragment" -->
* approche NLP <!-- .element: class="fragment" -->
* taches simples <!-- .element: class="fragment" -->

note:
* IntelliCode
* auto-complétion en fonction du contexte
* erreurs difficiles à identifier
* patterns / code stytle

---

## Conclusion
* Etapes d'un projet de data science <!-- .element: class="fragment" -->
* Outils <!-- .element: class="fragment" -->

note:
* la majorité du travail = collecter / nettoyer la data
* Codelab dense
