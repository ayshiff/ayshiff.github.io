---
layout: post
title: Workshops Competitive Programming - Part 5
---

Exemple d'un problème populaire d'optimisation combinatoire (voir plus).

## Activity selection problem

Prenons un exemple d'un problème populaire d'optimisation combinatoire.

Vous avez une liste d'activités à réaliser dans la journée (toutes définies par une heure de départ et de fin en heures), vous savez que vous ne pourrez pas toutes les faire.
Vous voudriez trouver le nombre maximale d'activités que vous pourriez réaliser dans la journée sans que les activités ne se superposent.

Prenez un moment pour réfléchir au problème et revenez lorsque vous aurez trouvé une solution.

**Solution**

Nous pouvons résoudre ce problème avec ce que l'on appelle un "algorithme gourmand" ou "greedy algorithm" en anglais.

**Algorithme**

Voici un **pseudo-code**:

```
Greedy-Iterative-Activity-Selector(A, s, f): 

    Sort A by finish times stored in f
    
    S = {A[1]} 
    k = 1
    
    n = A.length
    
    for i = 2 to n:
       if s[i] ≥ f[k]: 
           S = S U {A[i]}
           k = i
    
    return S
```

**Explication**

    - A est un tableau contenant les activités
    - s est un tableau contenant les heures de départs
    - f est un tableau contenant les heures de fin

1- Trier dans l'ordre croissant des heures de fin le tableau d'activité A.   

2- Créer un set S qui contiendra les activitées sélectionnées et initialiser-le avec l'activité A[1] qui correspond à l'activité qui a l'heure de fin la plus petite.   

3- Créer une variable k qui gardera l'index de la dernière activité selectionnée.   

4- Commencer à itérer à partir du deuxième élément du tableau A jusqu'à son dernier élément.

5- Pour chacun des élément du tableau, si l'heure de départ de l'activité est plus grande ou égale à l'heure de fin de la dernière activité selectionné (f[k]), alors nous pouvons l'ajouter au set S et changer l'index du dernier élément selectionné.

**Implémentation en C++**

```cpp
#include <bits/stdc++.h>
using namespace std;

void pairsort(vector<int>& a, vector<string>& b, int n) 
{ 
    pair<int, string> pairt[n]; 
  
    // Nous ajoutons les éléments des deux
    // tableaux dans des paris clé/valeurs
    for (int i = 0; i < n; i++)  
    { 
        pairt[i].first = a[i]; 
        pairt[i].second = b[i]; 
    } 
  
    // Trier la liste de pairs 
    sort(pairt, pairt + n); 
      
    // Modifier les tableaux originaux
    for (int i = 0; i < n; i++)  
    { 
        a[i] = pairt[i].first; 
        b[i] = pairt[i].second; 
    } 
}

set<string> Greedy_Iterative_Activity_Selector(vector<string> A, vector<int> s, vector<int> f) {
    int x = f.size();
    pairsort(f, A, x);

    set<string> S = {A[0]};
    int k = 0;
    int n = A.size();

    for(int i=1;i<n;i++) {
        if(s[i] >= f[k]) {
            S.insert(A[i]);
            k = i;
        }
    }
    return S;
}

int main() {
    vector<string> N = {"activity_4", "activity_2", "activity_3", "activity_1", "activity_5"};
    vector<int> end = {4,3,4,3,4};
    vector<int> begin = {2,2,3,2,1};

    set<string> finale = Greedy_Iterative_Activity_Selector(N, begin, end);

    cout << finale.size() << "\n";
}
```