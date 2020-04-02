---
layout: post
title: Workshops Competitive Programming - Part 3
---

Dans Cet article nous allons apprendre à planifier une approche (voir plus).

## Comment planifier une approche ?

Planifier une approche est une étape méticuleuse, elle peux aussi bien bloquer des développeurs expérimentés comme des débutants. Elle peut demander des calculs, de l'intuition, de la créativité et même de la chance.
Nous verrons dans cette section comment choisir une approche et résoudre le problème avec un plan solide.

**Pattern minning**

Il est facile de regarder les problèmes qui apparaissent dans les compétitions et de reconnaître certains pattern récurrents.
En effet, les problèmes ont souvent des similitudes avec ceux que vous auriez pu résoudre pendant vos entraînement.
Le pattern minning c'est ça ! S'entraîner sur le plus de cas possibles pour être en mesure lorsqu'un problème apparaît de se dire "J'ai déjà résolu un problème similaire et je sais comment le résoudre !".
Le point négatif de cette approche est que souvent le candidat pense avoir à faire à un problème qu'il a déjà rencontré alors qu'il s'agit d'un autre type d'énoncé.
Généralement on peut le voir dans les compétitions lorsqu'un problème vraiment original est proposé, la majorité des développeurs expérimentés ne réussissent pas à le résoudre.

**Coding Kata**

Voici votre **premier exercice** !
Prenez n'importe quel problème sur votre plateforme favorite (CodeChef, CodeForces...) que vous n'avez pas encore résolu.
Résolvez-le, peu importe le temps que ça vous prend.
Puis, notez le temps qu'il vous a fallu pour en venir à bout.
Maintenant, effacez votre solution et re-essayez de résoudre le problème.
(sans copier-coller évidemment !) Encore une fois, notez votre temps et refaite ce processus une dernière fois.

Le premier temps qu'il vous a fallu est le temps qu'il vous faut quand vous ne connaissez pas le type de problème et que vous n'avez aucune approche en tête.
Votre temps pour la deuxième phase est généralement le premier temps moins le temps qu'il vous a fallu pour comprendre le problème.
Enfin, le dernier temps est le temps que vous pourriez faire en compétition si vous aviez la bonne approche directement après avoir lu l'énoncé.
J'espère que ce temps vous encourage à vous entraîner !

Sur le même principe que les kata en arts martiaux, le principe est de répéter des pattern pour pouvoir reconnaître certains plans à mettre en place lorsque vous reconnaissez un problème familier.

**Tactiques d'approche**

Le plus important dans l'approche que vous aurez est de pouvoir se visualiser tout le cheminement de votre solution dans votre tête ou sur papier avant de passer au code. Comme si vous essayiez de vous persuader avant de coder que votre solution fonctionnera.
Les personnes ayant fait des maths reconnaîtront là une méthode familière.
Les joueurs d'échecs peuvent eux aussi reconnaître une méthode consistant à anticiper à l'avance différents mouvements futurs.

**Résoudre un problème**

Commencez par prototyper votre solution en commençant par la fonction principale puis les fonctions annexes.
Penser avec une approche atomique vous permettra de mieux vous organiser dons votre démarche.
Cette méthode fonctionne vraiment bien avec les problème récursifs.
L'idée générale derrière ce concept de récursivité et de pouvoir découper un problème en plusieurs sous-problèmes qui seront plus simples à résoudre.

**Comment débugger ?**

Dès que vous utilisez une approche, vous devez toujours avoir un plan pour débugger votre code. C'est toujours la partie compliquée. Le meilleur moyen d'éviter ces erreurs étant de réfléchir en amont aux cas particuliers dans lesquels votre code ne passera pas les tests.
Vous pouvez également segmenter votre code en mettant en avant les "zones à risques" où votre code risque de produire des erreurs.
L'autre avantage de découper son code en fonction est de pouvoir plus facilement trouver les zones à risque et de les corriger.

**Bottom Up Programming**

Cette technique devrait être la première que vous commenciez à faire dès que vous êtes bloqué. La programmation "ascendante" consiste à construire votre solution en partant des fonctions dont vous aurez besoin puis de remonter jusqu'à la solution finale.

**Conclusion**

Comme nous pouvons le voir, la pratique doit prendre une place importante dans votre entraînent.
Sans celle-ci, vous ne pourrez pas repérer les patterns récurrents.
