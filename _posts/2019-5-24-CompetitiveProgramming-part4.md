---
layout: post
title: Workshops Competitive Programming - Part 4
---

Dans Cet article nous allons introduire les mathématiques et graphes (voir plus).

## Les mathématiques pour les compétitions de programmation

Les mathématiques ont une place importante dans les problèmes posés.
Les candidats ayant une connaissance de certains concepts mathématiques utilisés partent avec un gros avantage sur le restes des autres candidats.
Je suis persuadé que les mathématiques ont une place importante dans ces compétitions puisque les mathématiques et les "Computer Sciences" vont généralement ensemble.

Les notions que nous pouvons souvent retrouvées dans les problèmes sont:   
- les nombres premiers 
- le plus grand diviseur commun (GCD) 
- le plus petit commun multiple (PPCM) 
- géométrie - bases (binaire...) 
- fractions et nombres complexes

Pour conclure cette section sur les mathématiques, je dirai que vous ne pourrez pas atteindre le haut du classement sans connaitre ces notions de mathématiques.

Voici quelques ressources (en anglais):

- https://www.amazon.comConcrete-Mathematics-Foundation-Computer-cience/dp/0201558025
- https://www.geeksforgeeks.orgmathematical-algorithms/

## Introduction aux Graph et leurs structures de données

Les graphs et arbres sont des structures de données fondamentales dans le monde de la programmation.
Leur utilisation est multiple et peut aller d'un problème où vous devez trouver un chemin dans une matrice d'un point A à B ou encore trouver la quantité maximale d'eau que vous pouvez acheminer à travers un ensemble de tuyau (dont chacun a une capacité maximale).
Connaître la structure de données adaptée au problème est primordiale !

![graph](https://upload.wikimedia.org/wikipedia/commons/thumb/d/d0/Arbre_binaire_ordonne.svg/1200px-Arbre_binaire_ordonne.svg.png)

**Reconnaître un problème de graphe**

Généralement, les problèmes utilisants des graphs on recours à des matrices ou réseau de noeuds ou des chemins.
Les mots clés associés que vous pouvez retrouver dans les problèmes : vertices, nodes, edges, connections, connectivity, paths, cycles, direction.

**Représenter le graphe**

Les graphs peuvent se représenter sous différentes formes, comme une matrice.
Nous avons tout d'abord besoin de savoir en quoi consiste un graph. En fait, il y a deux composants: les noeuds et arrêtes. Un noeud est une position dans le graphe alors qu'une arrête est un lien entre deux noeuds (qui peut avoir un poids ou non / être unidirectionnel ou non).

**Les arbres binaires**

Un arbres binaire peut se repésenter sous la forme d'un tableau à 1 dimension T[1..100].
La racine sera T[1], l'élément gauche de la racine sera T[2] et l'élément droit sera T[ 3 ].

Généralement, l'élément gauche d'un noeud N est T[N * 2] et le droit est T[N * 2 + 1].
Le parent d'un noeud est T[N / 2]

Tout dépend du type de graph dont vous avez besoin, vous pourrez avoir besoin de le représenter sous la forme d'une classe.
