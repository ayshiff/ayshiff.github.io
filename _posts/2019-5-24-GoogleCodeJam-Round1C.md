---
layout: post
title: Google Code Jam 2019 - Round 1C - Robot Programming Strategy
---

Cet article vous montre comment j'ai abordé un problème de la Google Code Jam (voir plus).

Voici l'énoncé du problème: [Robot Programming Strategy](https://codingcompetitions.withgoogle.com/codejam/round/00000000000516b9/0000000000134c90).

**Solution**

La solution peut être amélioré mais elle passe les deux jeux de tests et montre ma vision du problème. 

Concrêtement ce que fait le code : il remplit un tableau avec les instructions en input puis, il parcourt chaque élément pour rassembler dans un map / clé-valeur, index et charactères se trouvant à cette index dans chacunes des instructions (qui ont toute la taille de la plus longue instruction + 1).
En partant de là, nous itérons sur chacun des éléments de notre map en prenant en compte les différents cas possible.

Si nous avons pour le premier index, des "P" et "S", nous savons qu'il faut garder le "S" pour notre résultat finale (le ciseaux bat la feuille). Nous aurons donc les instructions avec le premier index "S" qui resterons tandis que celles avec des "P" ne seront plus pris en compte (nous les avons déjà battus).
Nous remplaçons donc leurs valeurs dans le map par des zéros pour indiquer quelles n'auront pas d'unfluence sur nos futurs choix.
(Imaginons que l'index du "P" dans le premier éléménent soit 2, nous remplacerons tous les éléments dans le map où l'index est égal à 2).

Concrêtement, pour chaque coup que nous jouons, nous cherchons soit à gagner, soit faire un nul.
Enfin, si les trois charactères sont présents dans les instructions restantes à un index t, cela signifie que nous ne pouvons pas trouver de solution et nous renvoyons "IMPOSSIBLE".

**Code C++**:


```cpp
#include <bits/stdc++.h>
#include <vector>
#include <string>

using namespace std;

string resize_string(string str, int size) {
    int increment = 0;
    while (str.size() != size) {
        if (increment == str.size()-1) increment = 0;
        str += str[increment];
        increment++;
    }
    return str;
}

void remove_element(char el, pair<int, vector<char>>& t,  map<int, vector<char>> arr) {
    for (int i=0;i< t.second.size();i++) {
        if (t.second[i] == el) {
            for (int l= t.first+1;l<arr.size();l++) {
                arr[l][i] = 0;
            }
        }
    }
}

int main() {
    ios::sync_with_stdio(false);
    int test_cases;
    cin >> test_cases;

    for(int t=1;t<=test_cases;t++) {
        int N, x, vn, len = 0;
        bool end = false;
        string finale = "";
        cin >> N;

        map<int, vector<char>> arr;
        vector<string> base;

        for(int i = 0;i<N;i++) {
            string value; cin >> value;
            if (value.size() > len) len = value.size();
            base.push_back(value);
        }

        for(int i = 0;i<N;i++) {
            if (base[i].size() < len+1) {
                base[i] = resize_string(base[i], len+1);
            }
        }

        for(int i = 0;i<N;i++) {
            string value = base[i];
            for (int test=0;test<value.size();test++) {
                arr[test].push_back(value[test]); 
            } 
        }

        for ( pair<int, vector<char>> t : arr) {
            if (!end) {
                if (find(t.second.begin(), t.second.end(), 'P') != t.second.end() && 
                    find(t.second.begin(), t.second.end(), 'R') != t.second.end() &&
                    find(t.second.begin(), t.second.end(), 'S') != t.second.end()) {
                        finale = "IMPOSSIBLE";
                        end = true;
                        break;
                } else if (find(t.second.begin(), t.second.end(), 'P') != t.second.end() && 
                    find(t.second.begin(), t.second.end(), 'R') != t.second.end()) {
                        finale += "P";
                        remove_element('R', t, arr);
                } else if (find(t.second.begin(), t.second.end(), 'P') != t.second.end() && 
                    find(t.second.begin(), t.second.end(), 'S') != t.second.end()) {
                        finale += "S";
                        remove_element('P', t, arr);
                } else if (find(t.second.begin(), t.second.end(), 'S') != t.second.end() && 
                    find(t.second.begin(), t.second.end(), 'R') != t.second.end()) {
                        finale += "R";
                        remove_element('S', t, arr);
                } else if (find(t.second.begin(), t.second.end(), 'R') != t.second.end()) {
                        finale += "P";
                        end = true;
                        break;
                } else if (find(t.second.begin(), t.second.end(), 'P') != t.second.end()) {
                        finale += "S";
                        end = true;
                        break;
                } else if (find(t.second.begin(), t.second.end(), 'S') != t.second.end()) {
                        finale += "R";
                        end = true;
                        break;
              }
            } else {
                break;
            }
        }

        cout << "Case #" << t << ": " << finale << "\n";
    }

}
```