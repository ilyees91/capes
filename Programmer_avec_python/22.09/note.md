# 22 septembre — Types abstraits et structures de données

[Ouvrir le cours et les exercices expliqués](cours.ipynb) · [TD 2 — Récursivité et structures immuables](TD2.pdf) · [TD 3 — Ensembles](TD3.pdf)

Le notebook rassemble les notes de séance et des compléments de révision. Les essais déjà présents sont expliqués et corrigés ; les ajouts pédagogiques servent à comprendre les notions, sans prétendre reconstituer les propos exacts du cours.

## Contenu

- **Types abstraits et représentations :** distinguer les opérations promises par un type de la structure choisie pour les réaliser.
- **Mutabilité et références :** comprendre les objets partagés, les tuples contenant des objets mutables et les arguments par défaut.
- **TD 2, exercice 1 :** calculer une somme récursivement, expliquer le coût des tranches, utiliser des indices et comprendre la limite de récursion.
- **TD 2, exercice 4 :** construire des listes immuables, calculer leur longueur et leur somme, les afficher et les inverser ; chaque correction est accompagnée de son raisonnement et de sa complexité.
- **TD 3, exercice 1 :** représenter un ensemble par des booléens, ajouter plusieurs valeurs, calculer leur somme et maintenir un cardinal en temps constant.

Des repères préparent les autres exercices, notamment le piège de `inv=[]` et la mesure de la mémoire. Les PDF restent les énoncés de référence.

## Pour travailler

Exécuter les cellules du notebook dans l'ordre, à partir d'un noyau neuf. Les exemples couvrent notamment la liste vide, les doublons et la différence entre somme et cardinal. L'expérience consistant à augmenter fortement la limite de récursion figure dans un bloc de texte séparé : l'exécution normale des cellules ne modifie pas cette limite.

Pour réviser, essayer d'abord de réécrire les fonctions sans regarder leur correction, puis expliquer pourquoi elles terminent et comment leur coût dépend de la taille de l'entrée.
