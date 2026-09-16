# Terminaison et correction : variants et invariants

*Cours du 16 septembre — notes à partir du tableau, complétées par des explications et un exemple d'invariant.*

Cette partie correspond aux questions de l'**exercice 2 du PDF « exercice Algo et complexité »** : proposer un variant pour prouver la terminaison, puis un invariant pour prouver la correction des algorithmes précédents.

## Deux questions différentes

| Question | Ce qu'on cherche à prouver | Outil courant |
| --- | --- | --- |
| L'algorithme finit-il par s'arrêter ? | La **terminaison** | Un **variant** |
| Renvoie-t-il le résultat attendu ? | La **correction** | Un **invariant de boucle**, ou une preuve par récurrence pour une fonction récursive |

La phrase « l'algorithme fait ce qu'il doit faire » signifie qu'il respecte sa **spécification** : pour les entrées autorisées, il produit le résultat annoncé.

Un algorithme peut s'arrêter et renvoyer un résultat faux. Réciproquement, une propriété décrivant correctement les calculs ne suffit pas à garantir qu'ils finissent.

- **Correction partielle** : si l'algorithme termine, son résultat est correct.
- **Correction totale** : il termine et son résultat est correct.

## 1. Le variant : prouver que l'exécution s'arrête

### Proposition du tableau

Pour une boucle, on cherche une quantité calculée à partir des variables, appelée **variant**, qui :

1. prend ses valeurs dans les **entiers naturels** ;
2. **décroît strictement** à chaque itération.

Pour une fonction récursive, on vérifie cette diminution entre un appel et chacun des appels récursifs qu'il effectue.

Il ne peut pas exister de suite infinie strictement décroissante d'entiers naturels. L'exécution ne peut donc pas continuer indéfiniment de cette façon. On suppose aussi que les opérations réalisées entre deux étapes terminent.

**« Positif » inclut ici zéro** : on peut arriver à un variant nul. Selon les conventions de vocabulaire, on dira plutôt « entier positif ou nul » pour éviter l'ambiguïté.

### Pourquoi les deux conditions sont-elles nécessaires ?

- Une quantité constante ne suffit pas : il faut une diminution **stricte**.
- Une quantité entière qui diminue sans borne inférieure ne suffit pas : $0,-1,-2,\ldots$ peut continuer indéfiniment.
- Une quantité réelle positive qui diminue strictement ne suffit pas non plus : $1,1/2,1/4,\ldots$ ne finit jamais par atteindre zéro en mathématiques.

### La généralisation écrite en rouge : un ordre bien fondé

Le professeur précise qu'on peut utiliser, plus généralement, un ensemble muni d'un **ordre bien fondé** : un ordre qui n'admet pas de chaîne strictement décroissante infinie.

Les entiers naturels avec l'ordre habituel en sont l'exemple principal. Pour les exercices simples, trouver un variant entier positif ou nul suffit généralement.

### Exemples ajoutés au tableau : l'ensemble et l'ordre comptent

Dire qu'un ensemble est « bien fondé » est un raccourci : c'est **l'ordre choisi sur cet ensemble** qui est bien fondé.

| Ensemble et ordre | Bien fondé ? | Explication |
| --- | --- | --- |
| $\mathbb N$ avec l'ordre habituel | Oui | On ne peut pas descendre strictement indéfiniment en restant dans les entiers naturels. |
| $\mathbb Z$ avec l'ordre habituel | Non | $-1>-2>-3>\cdots$ est une chaîne décroissante infinie. |
| Les réels positifs avec l'ordre habituel | Non | $0{,}1>0{,}01>0{,}001>\cdots$ reste positif et décroît indéfiniment. |
| Tous les mots finis sur un alphabet contenant `a < b`, avec l'ordre du dictionnaire | Non | `ab > aab > aaab > …` est une chaîne décroissante infinie. |
| $\mathbb N^2$ avec l'ordre lexicographique | Oui | On compare d'abord la première coordonnée, puis la seconde en cas d'égalité. |

**Pour les mots :** `aab` vient avant `ab`, car la première lettre est la même et, à la deuxième position, `a < b`. Ajouter un `a` avant le `b` produit à chaque fois un mot plus petit. Chaque mot est fini, mais leurs longueurs ne sont pas bornées. Un dictionnaire contenant seulement un nombre fini de mots ne permettrait pas une telle chaîne infinie.

### L'ordre lexicographique sur les couples d'entiers naturels

On définit :

$$
(i,j)<_{\mathrm{lex}}(k,\ell)
\quad\Longleftrightarrow\quad
i<k\ \text{ou}\ (i=k\ \text{et}\ j<\ell).
$$

La **première coordonnée est prioritaire**. Si elle diminue, la seconde peut augmenter : le couple a quand même diminué.

Exemple correspondant à l'idée du tableau :

$$
(2,3)>_{\mathrm{lex}}(2,2)>_{\mathrm{lex}}(2,1)
>_{\mathrm{lex}}(2,0)>_{\mathrm{lex}}(1,1000).
$$

Le dernier passage est bien une diminution : $1<2$, même si $1000>0$. En revanche, passer de $(2,3)$ à $(2,4)$ ne convient pas : la première coordonnée reste égale et la seconde augmente.

**Pourquoi cet ordre est-il bien fondé ?** Dans une chaîne strictement décroissante, la première coordonnée ne peut jamais augmenter. Comme c'est un entier naturel, elle ne peut diminuer qu'un nombre fini de fois ; si la chaîne était infinie, elle finirait donc par rester constante. À partir de là, la seconde coordonnée devrait diminuer strictement à chaque étape, indéfiniment dans $\mathbb N$, ce qui est impossible.

Cela ne contredit pas l'exemple des mots : dans $\mathbb N^2$, il y a **exactement deux coordonnées**. Dans la chaîne `ab`, `aab`, `aaab`, etc., le nombre de positions augmente sans limite.

### À quoi sert un variant à deux composantes ?

Un variant peut donc être un **couple** $V=(i,j)$ d'entiers naturels. Pour prouver la terminaison, il suffit de montrer qu'à chaque étape :

- soit `i` diminue strictement et `j` reste un entier naturel ;
- soit `i` reste inchangé et `j` diminue strictement.

Cela permet notamment de décrire un traitement par phases : `i` compte les phases restantes, et `j` le travail restant dans la phase courante. Lorsqu'on passe à la phase suivante, `i` diminue et `j` peut être réinitialisé à une grande valeur.

**La somme `i + j` n'est pas automatiquement un variant :** dans le passage de $(2,0)$ à $(1,1000)$, elle augmente de $2$ à $1001$, alors que le couple diminue pour l'ordre lexicographique.

> **À retenir :** un variant n'est pas nécessairement un seul entier. Ce qui compte est une diminution stricte dans un ordre qui interdit les chaînes décroissantes infinies.

## 2. Exemple du tableau : la fonction récursive `pair(n)`

La fonction teste si un **entier naturel** est pair. En Python, le test d'égalité s'écrit `==`.

```python
def pair(n):
    # Précondition : n est un entier positif ou nul.
    if n == 0:
        return True
    elif n == 1:
        return False
    else:
        return pair(n - 2)
```

### Prouver la terminaison

On choisit comme variant **la valeur de `n`**.

- Pour $n=0$ ou $n=1$, on renvoie directement un résultat : aucun appel récursif.
- Pour $n\geq2$, on appelle `pair(n - 2)`. Le nouveau paramètre est encore positif ou nul, et $n-2<n$.

Le variant reste donc dans les entiers naturels et décroît strictement à chaque appel récursif. La fonction atteint nécessairement $0$ ou $1$ et termine.

Exemples :

```text
pair(6) → pair(4) → pair(2) → pair(0) → True
pair(5) → pair(3) → pair(1) → False
```

**Attention au domaine :** l'annotation « pour n ≤ 1, pas d'appel » doit se lire sous l'hypothèse $n\geq0$ : ce sont alors uniquement les cas $0$ et $1$. Avec le code ci-dessus, un entier négatif ne rencontre aucun cas de base et les appels continuent vers des entiers toujours plus petits.

### Prouver que le résultat est correct

La terminaison ne prouve pas à elle seule que le booléen renvoyé est le bon. On raisonne ici **par récurrence forte sur $n$** :

1. **Cas de base :** $0$ est pair et la fonction renvoie `True` ; $1$ est impair et elle renvoie `False`.
2. **Hérédité :** pour $n\geq2$, supposons le résultat correct pour les entiers naturels strictement inférieurs à $n$. Il l'est donc pour $n-2$. Or $n$ et $n-2$ ont la même parité. Renvoyer `pair(n - 2)` donne donc la bonne réponse pour $n$.

La fonction termine et répond correctement sur le domaine annoncé : on a établi sa **correction totale**, dans le modèle mathématique d'exécution.

En pratique, Python limite la profondeur de récursion : une entrée trop grande peut provoquer une `RecursionError`. Cela ne remet pas en cause la preuve mathématique de terminaison, mais limite cette implémentation.

## 3. L'invariant : décrire ce qui reste vrai

Un **invariant de boucle** est une propriété vraie avant la première itération et conservée par chaque itération. On la formule à un point précis, généralement **au début de chaque tour**, lorsqu'on évalue la condition de boucle.

Les variables peuvent changer : c'est **la propriété** qui reste vraie, pas forcément leurs valeurs.

### Les trois étapes d'une preuve

1. **Initialisation :** montrer que la propriété est vraie avant le premier tour.
2. **Conservation :** supposer qu'elle est vraie au début d'un tour et montrer qu'elle reste vraie après ce tour.
3. **Conclusion à la sortie :** combiner l'invariant et la condition de sortie pour obtenir le résultat attendu.

Un invariant quelconque ne suffit pas : il doit être assez précis pour permettre cette dernière étape. La terminaison se prouve séparément, par exemple avec un variant.

### Exemple complémentaire : somme des diviseurs

Cet exemple reprend la question 7, sous forme de boucle `while` pour rendre les étapes visibles. Ce n'est pas une transcription supplémentaire de la photo.

```python
def somme_div(n):
    # Précondition : n est un entier strictement positif.
    s = 0
    i = 1
    while i <= n:
        if n % i == 0:
            s += i
        i += 1
    return s
```

**Invariant au début de chaque tour et à la sortie :**

> $1\leq i\leq n+1$, et `s` est la somme des diviseurs de $n$ compris entre $1$ et $i-1$.

Autrement dit, `s` contient exactement les diviseurs **déjà examinés**.

- **Initialisation :** `i = 1`. Aucun entier n'a encore été examiné ; la somme vide vaut $0$, qui est bien la valeur de `s`.
- **Conservation :** on examine `i`. S'il divise $n$, on l'ajoute ; sinon, on ne change pas `s`. Puis on incrémente `i`. La somme contient donc exactement les diviseurs strictement inférieurs à la nouvelle valeur de `i`, et les bornes restent respectées.
- **Sortie :** la condition `i <= n` est fausse. Avec l'invariant, on obtient `i = n + 1`. La variable `s` contient donc tous les diviseurs de $n$ entre $1$ et $n$ : c'est la somme recherchée.

**Variant de cette même boucle :** $V=n-i+1$. Au début, il vaut $n$. Il diminue de $1$ à chaque tour et reste positif ou nul ; à la sortie, il vaut $0$. Cela prouve la terminaison.

## Méthode à retenir pour les exercices

1. Préciser le **domaine des entrées** et le **résultat attendu**.
2. Pour la terminaison, donner un variant et vérifier son domaine ainsi que sa décroissance stricte.
3. Pour une boucle, formuler un invariant, puis prouver initialisation, conservation et conclusion à la sortie.
4. Pour une fonction récursive, justifier les cas de base et la correction des appels plus petits par récurrence.

> **Variant : « pourquoi ça s'arrête ». Invariant : « ce qui reste vrai et permet de prouver le résultat ». Les deux arguments se complètent.**
