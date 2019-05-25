---
layout: post
title: Workshops Competitive Programming - Part 2
---

Dans Cet article nous allons apprendre à comprendre le problème posé et trouver une solution (voir plus).

## Comment comprendre l'énoncé d'un problème ?

Regardons la composition de l'énoncé d'un problème.

Pour commencer nous avons l'introduction avec une mise en contexte d'un problème de la vie de tous les jours, fiction...
Pour la majorité des cas, la compréhension du contexte n'est pas particulièrement importante à la résolution du problème.

Deuxièmement, nous avons la partie avec la définition de la solution. Cela vous donne le squelette de la solution que vous aurez à écrire.

Vous pourrez également avoir des notes sur des notions utiles à avoir (des formules mathématiques,...).

Ensuite nous avons la partie avec les contraintes. Cette section est une des plus importantes puisque-elle vous permet de savoir à quel point votre algorithmes devra être performant pour passer les tests.

Finalement, nous avons un jeu de tests d'exemple qui va nous permettre de tester notre programme. Vous aurez dans l'ordre, les inputs, les valeurs de retour attendues, puis, optionnellement, une explication des données de tests.

## Comment trouver une solution ?

Généralement les problèmes ont des traits en commun, les solutions peuvent donc être trouvées assez rapidement en lisant l'énoncé du problème.
Ces traits communs sont des indices cruciaux pour les personnes expérimentées qui sont capables de les reconnaître.

## Différents types de problèmes

**Straight-forward problems**
Les problèmes qui ne demandent pas de techniques particulière:
il s'agit des problèmes demandant seulement au programme d'exécuter une série d'opérations pas à pas.

**Breadth First Search**
Généralement ces problèmes demandent de trouver le chemin le plus court, avec le minimum d'étapes,... avec des matrices, graphs,...
La complexité de ces problèmes est généralement linéaire.

**Backtracking / Brute Force**
Ces techniques peuvent être utilisées dans différents types de problèmes comme ceux qui vous demandent de trouver toutes les configurations possibles d'éléments en respectant certaines contraintes ou de trouver la configuration optimale respectant des règles fixées. (ex: sudoku)
Le backtracking est quant à lui plus optimisé que le brute-force.

<p align="center">
<img alt="backtracking" src="https://www.researchgate.net/profile/Ilya_Verenich/publication/316610194/figure/fig2/AS:614206495813635@1523449648050/Backtracking-algorithm-taken-from-1.png" width="300"/>
</p>

**Dynamic Programming**
Une bonne partie des problèmes peuvent être résolus grâce à cette technique.
Savoir quand l'utiliser peut être vraiment avantageux ! Le principe de base est de découper un problème complexe en un sous-ensemble de problèmes plus petits à résoudre, qui une fois résolus ammenent à la solution finale.

<p align="center">
<img alt="dynamic-programming" src="https://cdn-images-1.medium.com/max/1600/1*MXpfyivX8XmtULGNiXXmEw.png" width="300"/>
</p>

**Flood Fill**
Cette algorithme de remplissage par diffusion est fréquemment utilisé dans la manipulation de matrices. Il trouve également son application dans certains jeux comme le démineur.

<div style="display: flex; justify-content: center;">
<img alt="flood-fill" src="https://he-s3.s3.amazonaws.com/media/uploads/0435c22.png" height="200"/>
</div>