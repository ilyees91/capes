# Questions d’éducation — Enseigner et comprendre les apprentissages

> **Cours du 16 septembre.** Notes reformulées et complétées pour la révision. Les exemples en NSI sont des illustrations ajoutées ; ils ne constituent pas une transcription du cours.

## 1. Pédagogie et didactique : deux points de vue complémentaires

La **pédagogie** s’intéresse à la manière d’organiser l’enseignement et la relation éducative : faire travailler un groupe, accompagner les élèves, maintenir leur engagement, choisir des modalités d’évaluation, développer leur autonomie.

La **didactique d’une discipline** étudie l’enseignement et l’apprentissage de ses contenus : quels savoirs enseigner, dans quel ordre, avec quelles représentations et quels obstacles pour les élèves ?

La différence ne se résume donc pas à « une matière contre toutes les matières ». Les deux approches se croisent dans chaque séance.

**Exemple en NSI :** pour enseigner l’affectation, le professeur anticipe la confusion entre `x = x + 1` en Python et une égalité mathématique : c’est une question didactique. Il organise ensuite des binômes, distribue les rôles et prévoit des aides : ce sont des choix pédagogiques.

## 2. Le contrat didactique et la relation entre professeur et élèves

### Des attentes réciproques, souvent implicites

Le **contrat didactique**, notion développée par Guy Brousseau, désigne les attentes réciproques qui organisent les responsabilités du professeur et des élèves **à propos du savoir**. Une grande partie reste implicite : ce que l’élève croit devoir chercher, les aides qu’il attend, les justifications que le professeur considère comme nécessaires. Ce contrat peut évoluer ou être mis en difficulté par une nouvelle situation. Voir les [textes de Brousseau sur le contrat didactique](https://ardm.eu/guy-brousseau/guy-brousseau.com/tag/contrat-didactique/index.html).

**Exemple :** si tous les exercices de programmation précédents admettaient une solution avec la dernière boucle étudiée, les élèves peuvent croire qu’il faut toujours utiliser cette boucle. Une nouvelle activité peut exiger de choisir une autre méthode. Le professeur doit alors faire comprendre que l’objectif est de sélectionner un outil adapté, et pas seulement de deviner son attente.

À distinguer de deux autres éléments :

- le **cadre pédagogique**, qui organise le travail, les prises de parole ou l’entraide ;
- le **règlement intérieur**, document explicite de l’établissement relatif à la vie collective.

Le contrat didactique n’est donc pas un contrat signé entre l’enfant et l’établissement.

### Une relation dissymétrique, mais réciproque

La **dissymétrie** signifie que les rôles et les responsabilités ne sont pas identiques. Le professeur choisit les situations, possède une expertise disciplinaire, organise la progression et évalue. Il a une responsabilité particulière dans les conditions de l’apprentissage.

La **réciprocité** signifie que chacun agit sur la relation : les réponses, erreurs et questions des élèves informent le professeur, qui adapte ses explications ; les élèves doivent pouvoir comprendre les attentes et s’engager dans l’activité proposée.

**Exemple :** l’élève essaie d’expliquer pourquoi son programme échoue ; le professeur l’écoute, repère l’obstacle et apporte un indice utile. Donner immédiatement toute la solution peut faire disparaître le travail intellectuel attendu. À l’inverse, refuser toute aide peut laisser l’élève dans l’impasse.

> Les rôles diffèrent, mais le respect est réciproque. L’autorité pédagogique implique aussi une responsabilité d’accompagnement.

## 3. Daniel Kahneman : intuition, raisonnement et biais cognitifs

Le nom à retenir est **Daniel Kahneman**, psychologue qui a notamment travaillé avec **Amos Tversky** sur le jugement et la décision. Il est mort le **27 mars 2024** : mieux vaut retenir cette date que « l’année dernière ». Voir sa [notice sur le site du prix Nobel](https://www.nobelprize.org/prizes/economic-sciences/2002/kahneman/facts/).

### Deux modes de traitement de l’information

Kahneman distingue deux grands modes, souvent appelés **système 1** et **système 2**. Ce sont des catégories de fonctionnement, pas deux organes séparés du cerveau.

| Mode | Caractéristiques | Exemple ajouté |
| --- | --- | --- |
| Pensée intuitive — système 1 | Rapide, automatique, fondée sur des associations et des habitudes. | Reconnaître immédiatement une structure de code familière. |
| Pensée délibérée — système 2 | Plus lente, contrôlée, mobilisant de l’attention. | Tracer ligne par ligne les valeurs des variables pour vérifier un résultat. |

L’intuition peut être juste, notamment chez une personne expérimentée. Un raisonnement lent peut aussi comporter des erreurs. La distinction ne correspond donc pas exactement à « vécu contre science » : des connaissances apprises peuvent devenir automatiques. Voir la [conférence de Kahneman sur la rationalité limitée](https://www.nobelprize.org/prizes/economic-sciences/2002/kahneman/lecture/).

### Qu’est-ce qu’un biais cognitif ?

Un **biais cognitif** est une tendance systématique à déformer un jugement dans certaines conditions. Il ne se définit pas simplement comme l’écart entre intuition et savoir scientifique.

Quelques exemples pour comprendre les termes :

- **Biais de confirmation :** chercher surtout ce qui confirme son hypothèse. En programmation, ne tester que les entrées pour lesquelles on pense que le programme fonctionne.
- **Ancrage :** accorder trop de poids à une première information. Une première estimation du temps nécessaire à un projet peut influencer toutes les suivantes.
- **Disponibilité :** juger une situation à partir d’exemples faciles à se rappeler. Un incident marquant peut conduire à surestimer sa fréquence.

Pour travailler ces difficultés en NSI, on peut faire formuler une prédiction, demander une justification, puis chercher un **contre-exemple** et confronter le résultat à la prédiction. L’erreur devient une information à analyser.

## 4. Différencier l’enseignement

La **différenciation pédagogique** consiste à adapter les situations, les aides ou l’organisation du travail à des besoins repérés, pour faire progresser les élèves vers des objectifs d’apprentissage communs.

Elle peut porter sur les supports, le degré de guidage, les étapes, le temps ou les regroupements. Elle demande d’observer ce que les élèves savent déjà faire. Les groupes doivent pouvoir évoluer ; un élève en difficulté sur une notion ne doit pas être enfermé dans une catégorie définitive. Voir le [dossier du Cnesco sur la différenciation pédagogique](https://www.cnesco.fr/fr/ressources/dossier-synthese-differenciation-pedagogique/).

**Exemple en NSI : objectif commun — comprendre une boucle.**

- Certains élèves disposent d’un tableau de trace partiellement rempli.
- D’autres construisent seuls leur tableau.
- Ceux qui maîtrisent déjà l’exercice expliquent pourquoi la boucle termine ou cherchent un cas limite.

Tous reviennent ensuite à une synthèse commune. La différence porte sur l’aide et l’approfondissement, sans retirer aux élèves fragiles le raisonnement essentiel.

## 5. Évaluer : diagnostiquer, faire progresser, établir un bilan

Une **évaluation** recueille des informations sur les acquis ; une **note** n’est qu’une manière possible d’en communiquer le résultat.

| Fonction | But principal | Exemple en NSI |
| --- | --- | --- |
| **Diagnostique** | Repérer les acquis et les difficultés pour adapter l’enseignement. | Quelques questions sur variables et conditions avant d’aborder les boucles. |
| **Formative** | Aider l’élève à progresser et le professeur à ajuster son enseignement. | Un exercice suivi d’un retour précis et d’une nouvelle tentative. |
| **Sommative** | Faire le bilan des acquis après une période d’apprentissage. | Un devoir sur les boucles avec des critères annoncés. |
| **Certificative** | Attester officiellement un niveau ou valider une qualification. | Une épreuve contribuant à la délivrance d’un diplôme. |

Ces fonctions sont définies dans la [terminologie de l’éducation publiée au Bulletin officiel](https://www.education.gouv.fr/bo/2007/33/CTNX0710380K.htm). Elles peuvent se combiner : un bilan sommatif peut ensuite servir de support à un travail formatif.

Une évaluation devient réellement **formative** quand son résultat permet une action. « 8/20, insuffisant » renseigne peu sur la façon de progresser. « L’initialisation est correcte, mais l’accumulateur est remis à zéro dans la boucle ; déplace cette instruction puis teste sur trois valeurs » fournit une piste exploitable.

Le mot **formatrice**, également possible en pédagogie, insiste sur la participation de l’élève à sa propre évaluation : comprendre les critères, repérer ses erreurs et choisir comment les corriger. Il ne faut donc pas le remplacer automatiquement par « formative » sans vérifier le terme employé en cours.

## 6. La surcharge cognitive

La **mémoire de travail** maintient et traite temporairement les informations nécessaires à une tâche. Sa capacité est limitée pour les informations nouvelles. La **mémoire à long terme** contient des connaissances organisées qui rendent certaines opérations plus faciles ou automatiques.

Il y a **surcharge cognitive** lorsque les exigences simultanées d’une tâche dépassent les ressources disponibles. Une difficulté peut venir de la complexité de ce qu’il faut apprendre, mais aussi d’une consigne confuse ou de multiples informations à chercher dans des endroits différents. Voir la [synthèse du CESE sur la charge cognitive](https://education.nsw.gov.au/about-us/education-data-and-research/cese/publications/literature-reviews/cognitive-load-theory.html).

**Exemple :** découvrir en même temps un environnement de programmation, la syntaxe Python, les listes et un algorithme de tri impose de traiter beaucoup de nouveautés.

Pour faciliter le travail :

1. vérifier les prérequis ;
2. introduire les nouveautés par étapes ;
3. présenter un exemple résolu et expliquer les choix ;
4. proposer un exercice proche avec une aide partielle ;
5. retirer progressivement l’aide et demander une résolution autonome.

L’objectif est de préserver les ressources nécessaires pour comprendre, pas de supprimer toute difficulté.

## 7. Transmission, instructionnisme et constructivisme

### Un mot des notes reste à confirmer

Les notes indiquaient « intuitionnisme » pour l’idée qu’un élève ne découvre pas nécessairement seul ce qu’il doit apprendre. **Cette phrase ne suffit pas à identifier le courant évoqué.** Le mot attendu était peut-être **instructionnisme**, mais cette correction reste une hypothèse. L’intuitionnisme désigne notamment un courant de philosophie des mathématiques ; ce n’est pas ici un synonyme évident d’enseignement explicite.

### Deux questions à distinguer

Dans une approche centrée sur l’**instruction**, le professeur organise les contenus, explique les procédures, propose de l’entraînement et vérifie la compréhension. Cela ne suppose pas que l’élève soit intellectuellement passif.

Le **constructivisme**, associé notamment à Jean Piaget, décrit l’apprentissage comme une construction active : le sujet interprète une situation à partir de ce qu’il sait déjà et réorganise ses connaissances lorsqu’elles ne suffisent plus. Voir [Piaget, *Psychologie et pédagogie*, 1969](https://www.unige.ch/piaget/piaget1969PPE_02).

Une théorie de la construction des connaissances ne prescrit pas automatiquement de laisser les élèves tout découvrir sans guidage. **L’activité de l’élève et l’aide du professeur peuvent se compléter.**

**Exemple :** un élève pense que `=` signifie toujours « est égal à ». Le professeur lui fait prédire l’effet de `x = x + 1`, montre une trace d’exécution et explique l’affectation. L’élève doit reconstruire sa compréhension ; le professeur accompagne cette reconstruction.

## 8. Repères historiques évoqués en cours

### Les recherches américaines sur l’éducation

Les années 1920 ne marquent pas leur commencement. **John Dewey fonde une école laboratoire à Chicago en 1896**, où il met à l’épreuve ses conceptions éducatives. L’expérimentation pédagogique américaine est donc déjà organisée avant 1920. Voir l’[histoire des Laboratory Schools de Chicago](https://www.ucls.uchicago.edu/about-lab/history).

### Shannon : relier logique et circuits électriques

**Claude Shannon** montre comment l’algèbre de Boole peut servir à analyser et concevoir des circuits à relais et interrupteurs. Ses travaux menés à la fin des années 1930 donnent lieu à l’article **« A Symbolic Analysis of Relay and Switching Circuits » en 1938**. Voir l’[article de Shannon](https://doi.org/10.1109/T-AIEE.1938.5057767) et le [mémoire conservé au MIT](https://dspace.mit.edu/handle/1721.1/11173).

Pour comprendre le lien, on peut choisir de représenter un interrupteur fermé par `1` et ouvert par `0` :

- deux interrupteurs **en série** ne laissent passer le courant que s’ils sont tous deux fermés : comportement d’un **ET** ;
- deux interrupteurs **en parallèle** laissent passer le courant si au moins l’un est fermé : comportement d’un **OU**.

Cette correspondance permet de représenter et de simplifier mathématiquement des circuits. Elle est fondamentale pour comprendre la logique des systèmes numériques.

### Cybernétique et conférences Macy

La série de conférences Macy consacrée à la cybernétique se déroule de **1946 à 1953**, et non en 1958. Elle rassemble des chercheurs de plusieurs disciplines autour des systèmes, de la communication et de la **rétroaction**. Voir les [actes des conférences Macy](https://press.uchicago.edu/ucp/books/book/distributed/C/bo269830784.html).

Une rétroaction est un retour d’information sur l’effet d’une action qui permet de modifier l’action suivante. Un thermostat en fournit un exemple simple : il mesure la température et adapte le chauffage.

**Analogie pédagogique ajoutée :** le professeur propose une activité, observe les réponses, puis adapte la suite. Cette comparaison éclaire la notion de régulation ; elle ne réduit pas un élève à une machine.

## À retenir pour réviser

- **Didactique :** les contenus, leur apprentissage et leurs obstacles ; **pédagogie :** les conditions et l’organisation de l’enseignement.
- **Contrat didactique :** des attentes réciproques relatives au savoir, souvent implicites.
- **Différenciation :** ajuster les aides à des besoins repérés.
- **Formative :** faire progresser ; **sommative :** établir un bilan.
- **Charge cognitive :** organiser les nouveautés et retirer progressivement le guidage.
- **Kahneman :** intuition et raisonnement délibéré sont utiles, mais aucun n’est infaillible.
- **Point à confirmer :** le terme exact entendu à la place d’« intuitionnisme ».
