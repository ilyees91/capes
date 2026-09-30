# Terminaison et preuves de correction

**Analyse et résolution de problèmes · 23 septembre 2026 · TD 2**

[TD 2 avec la racine corrigée](TD2_erreur_corrige.pdf) · [Énoncé original](TD2_original.pdf) · [Notebook de travail](exercietd2.ipynb) · [Cours du 16 septembre](../16.09/cours_variants_invariants.md)

> **L'essentiel** — Un **variant** explique pourquoi un algorithme s'arrête. Un **invariant** décrit ce qui reste vrai pendant une boucle et permet de justifier son résultat.

**Origine des notes.** Les codes de l'exercice 1 viennent du PDF, remis en forme en Python. Les encadrés **Au tableau** reprennent les éléments lisibles des photos. Les preuves détaillées, traces et remarques sont des **compléments explicatifs** ; ils ne sont pas présentés comme une transcription du professeur. Certaines annotations à droite de la dernière photo sont coupées.

## Sommaire

- [1. La méthode : variant et invariant](#methode)
- [2. Les premiers exemples du tableau](#tableau)
- [3. Correction du TD 2 dans le notebook](#exercice1)
- [4. Ackermann : un variant à deux composantes](#ackermann)
- [5. Concevoir un algorithme à partir d'un invariant](#suite)
- [6. Fiche de révision](#revision)

---

<a id="methode"></a>
## 1. La méthode : variant et invariant

### Prouver la terminaison

**Au tableau :** on cherche une expression des variables, entière, strictement décroissante à chaque étape et positive ou nulle tant que l'exécution continue.

Pour une boucle, la preuve suit trois étapes :

| Étape | Question à traiter |
| --- | --- |
| Domaine | Pourquoi le variant est-il entier et minoré, par exemple par 0 ? |
| Décroissance | Comment évolue-t-il après un tour ? Montrer `V' < V`. |
| Conclusion | Une suite infinie strictement décroissante d'entiers naturels est impossible. |

Pour une fonction récursive, on compare le variant de l'appel courant à celui de **chaque appel récursif**. Il faut aussi que les opérations d'un tour ou d'un appel terminent elles-mêmes.

**Pourquoi des entiers ?** La suite réelle `1, 1/2, 1/4, …` reste positive et diminue strictement sans s'arrêter. À l'inverse, une suite entière `0, -1, -2, …` diminue sans borne inférieure : elle ne convient pas non plus.

### Prouver la correction

Un invariant est une **propriété**, pas nécessairement une valeur constante. On le formule à un endroit précis, en général au moment de tester la condition de boucle.

1. **Initialisation :** il est vrai avant le premier tour.
2. **Conservation :** s'il est vrai avant un tour, il l'est encore après ce tour.
3. **Sortie :** l'invariant et la négation de la condition de boucle donnent le résultat attendu.

| Notion | Ce qui est établi |
| --- | --- |
| Correction partielle | Si l'algorithme termine, il donne le bon résultat. |
| Terminaison | L'exécution finit. |
| Correction totale | L'algorithme termine et donne le bon résultat. |

Les preuves supposent des **préconditions** : entrées naturelles, diviseur strictement positif, tableau non vide, etc. Elles décrivent un modèle mathématique sans limite de mémoire ; Python peut notamment atteindre sa limite de récursion.

### Exemple complet : une division par soustractions

On veut diviser un entier naturel `a` par un entier `b > 0`. On commence avec `q = 0` et `r = a`, puis, tant que `r >= b`, on remplace `r` par `r - b` et `q` par `q + 1`.

- **Variant :** `r` est naturel et diminue de `b > 0` à chaque tour. La boucle termine.
- **Invariant :** `a = b*q + r`, avec `q >= 0` et `r >= 0`. Il est vrai au départ. Après un tour, `b*(q+1) + (r-b) = b*q+r = a` ; les nouvelles valeurs restent naturelles.
- **Sortie :** la condition est fausse, donc `r < b`. Avec l'invariant, on obtient `a = b*q+r` et `0 <= r < b` : ce sont les propriétés du quotient et du reste recherchés.

Pour `a = 17` et `b = 5`, les couples `(q, r)` sont `(0, 17)`, `(1, 12)`, `(2, 7)`, puis `(3, 2)`. Le variant explique l'arrêt ; l'invariant explique pourquoi le résultat `(3, 2)` est correct.

<a id="tableau"></a>
## 2. Les premiers exemples du tableau

### Parité récursive

```python
def pair(n):
    # Précondition : n est un entier naturel.
    if n == 0:
        return True
    elif n == 1:
        return False
    else:
        return pair(n - 2)
```

**Variant :** `n`. L'appel récursif n'a lieu que pour `n >= 2` ; le nouveau paramètre `n - 2` est naturel et strictement inférieur à `n`.

```text
pair(6) → pair(4) → pair(2) → pair(0) → True
pair(5) → pair(3) → pair(1) → False
```

**Complément — correction :** les deux cas de base sont corrects et `n` a la même parité que `n - 2`. Une récurrence forte établit la correction. La précondition est essentielle : avec un entier négatif, on s'éloigne des cas de base.

### Inverser un tableau sur place

```python
def miroir(tab):
    i = 0
    j = len(tab) - 1
    while j > i:
        tab[i], tab[j] = tab[j], tab[i]
        i = i + 1
        j = j - 1
```

**Au tableau :** le variant proposé est `j - i`. Tant que `j > i`, il est entier strictement positif. Après un tour :

$$V' = (j-1)-(i+1) = V-2 < V.$$

| Moment du test | `i` | `j` | `j - i` | Tableau |
| --- | --- | --- | --- | --- |
| Départ | 0 | 4 | 4 | `[1, 2, 3, 4, 5]` |
| Après un tour | 1 | 3 | 2 | `[5, 2, 3, 4, 1]` |
| Sortie | 2 | 2 | 0 | `[5, 4, 3, 2, 1]` |

**Précision :** pour une longueur paire, `j - i` finit à `-1`. Ce n'est pas un problème : la boucle s'arrête alors. Si l'on veut une expression naturelle même à la sortie, choisir `max(0, j - i)`.

**Complément — invariant :** les cases avant `i` et après `j` sont déjà à leur position finale ; la zone entre les deux indices est encore inchangée, et `i + j = len(tab) - 1`. Chaque échange place deux éléments symétriques. À la sortie, il reste au plus l'élément central, déjà bien placé.

Pour rendre « position finale » précis, noter `A` le tableau initial et `N = len(tab)` : une case déjà traitée d'indice `p` contient `A[N - 1 - p]`. Une liste vide ou de longueur 1 ne nécessite aucun échange et est déjà son propre miroir. Dans cette preuve, `A` est une référence mathématique au contenu initial ; le programme n'en fabrique pas de copie.

```python
tab = [1, 2, 3, 4]
miroir(tab)
print(tab)  # [4, 3, 2, 1]
```

La fonction modifie la liste et renvoie implicitement `None`. Elle effectue `len(tab) // 2` échanges : temps **O(n)**, espace supplémentaire **O(1)**.

---

<a id="exercice1"></a>
## 3. Correction du TD 2 dans le notebook

La correction détaillée est dans [exercietd2.ipynb](exercietd2.ipynb) : code exécutable, variants, preuves de terminaison et de correction, ainsi que tes notes initiales conservées. Exécuter les cellules dans l'ordre pour disposer des fonctions avant les exemples.

**Point à vérifier dans l'énoncé :** la version originale de `racineApprochee` contient une erreur. La version corrigée met à jour `s` avant `c` et renvoie `c - 1`. L'invariant `s = c²` s'applique à cette version corrigée ; le résultat est la partie entière de la racine carrée de `n`.

<a id="ackermann"></a>
## 4. Ackermann : un variant à deux composantes

Pour certaines fonctions récursives, aucun des paramètres pris isolément ne décroît à chaque appel. On peut alors utiliser un couple de naturels et un **ordre bien fondé**, c'est-à-dire un ordre qui n'admet aucune suite infinie strictement décroissante.

Pour Ackermann, on compare `(m, n)` dans l'**ordre lexicographique** : la première coordonnée est prioritaire ; à première coordonnée égale, on compare la seconde. Par exemple, `(1, 1000) < (2, 3)` et `(2, 2) < (2, 3)`.

L'appel `ackermann(m - 1, ackermann(m, n - 1))` demande deux justifications :

1. L'appel intérieur porte sur `(m, n - 1)`, plus petit que `(m, n)`. L'hypothèse de récurrence garantit qu'il termine et renvoie un naturel `r`.
2. L'appel extérieur porte alors sur `(m - 1, r)`, également plus petit, quelle que soit la taille de `r`.

La preuve complète et les cas de base se trouvent dans le notebook. **Terminer en théorie ne garantit pas un calcul réalisable rapidement** : la profondeur de récursion et le nombre d'appels peuvent devenir très grands.

<a id="suite"></a>
## 5. Concevoir un algorithme à partir d'un invariant

L'invariant peut servir à construire le programme : on décrit une partie déjà traitée et une partie restant à examiner, puis on choisit une opération qui agrandit la première sans casser ses propriétés.

| Problème du TD | Partie déjà traitée | Progression |
| --- | --- | --- |
| Somme ou minimum | Un préfixe dont on connaît la somme ou le minimum | Lire la case suivante |
| Tri par sélection | Les plus petits éléments, triés en début de tableau | Chercher le minimum de la zone restante |
| Tri par insertion | Un préfixe trié | Insérer la valeur suivante à la bonne place |
| Tri à bulles | Un suffixe contenant les plus grands éléments à leur place | Faire remonter un maximum par échanges voisins |
| Classement des élèves | Des secondes à gauche, puis des premières, et des terminales à droite | Réduire la zone encore inconnue |

Pour un tri, il faut prouver **l'ordre et la conservation des éléments**, répétitions comprises. Un programme qui remplace toutes les valeurs par zéro produit bien une liste ordonnée, mais ne trie pas l'entrée.

Le notebook propose maintenant les programmes des exercices 2 et 3, leurs invariants, des preuves et des exemples. Le code de classement utilise la méthode `niveau()` des objets élèves, conformément au PDF : `2` pour seconde, `1` pour première et `0` pour terminale.

<a id="revision"></a>
## 6. Fiche de révision

| Algorithme | Variant | Résultat ou propriété clé |
| --- | --- | --- |
| `pair(n)` | `n` | Même parité que `n - 2` |
| `miroir(tab)` | `j - i`, positif sous la condition de boucle | Extrémités déjà à leur position finale |
| `facto(n)` | `n` | `f × n! = N!` |
| `programmeMystere1` | Nombre d'éléments restant à lire | Positifs ou nuls à gauche, négatifs à droite |
| `racineApprochee(n)` | `n - s`, positif ou nul sous la condition | `s = c²` ; résultat `⌊√n⌋` (code corrigé) |
| `programmeMystere2` | `j - i` | Un maximum reste dans l'intervalle |
| Division euclidienne | `r`, pour `b > 0` | `a = bq + r`, puis `0 <= r < b` |
| PGCD | Second argument `b` | `0 <= a % b < b` pour `b > 0` |
| Ackermann | `(m, n)` dans l'ordre lexicographique | Chaque appel utilise un couple plus petit |
| Classement des élèves | `k - j + 1` | Quatre zones, dont une zone inconnue qui rétrécit |

### Pièges à éviter

- Confondre un variant et un invariant.
- Oublier les préconditions ou les cas vides.
- Proposer un variant décroissant mais non minoré.
- Déduire le résultat du seul nom d'une fonction.
- Oublier de justifier un appel récursif imbriqué.
- Présenter quelques tests comme une preuve valable pour toutes les entrées.

### Questions pour vérifier que le cours est compris

1. Pourquoi `s` n'est-il pas un variant décroissant de `racineApprochee` ? Il augmente ; sous la condition de boucle, `n - s` est un candidat adapté.
2. Pourquoi préciser que le tableau de `programmeMystere2` est non vide ? La fonction renvoie `tab[i]`, ce qui serait impossible sur une liste vide.
3. Pourquoi un invariant vrai ne suffit-il pas à garantir l'arrêt ? Il décrit un état, sans imposer de progression ; il faut une preuve de terminaison.
4. Pourquoi ne pas avancer `j` après avoir envoyé une terminale à droite ? L'élève ramené dans la case `j` vient de la zone inconnue et doit encore être examiné.
