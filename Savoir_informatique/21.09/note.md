# 21 septembre — Prérequis pour étudier les graphes et le routage

**Question de départ : de quoi un élève a-t-il besoin pour comprendre comment un paquet circule dans un réseau ?**

Les notes initiales mentionnaient les adresses IP. Cette fiche développe les prérequis associés et propose une progression pédagogique. Les exemples sont des compléments de révision.

## 1. Distinguer les deux objets d'étude

Un **graphe** est un modèle mathématique qui représente des objets et leurs relations. Il peut décrire un réseau informatique, mais aussi des villes reliées par des routes ou les dépendances entre des tâches. On peut donc apprendre les graphes sans connaître les adresses IP.

Le **routage** consiste à déterminer comment acheminer des paquets vers leur destination à travers plusieurs réseaux. Pour le comprendre, on combine des connaissances sur les réseaux et sur les graphes.

| Pour commencer les graphes | Pour appliquer les graphes au routage |
| --- | --- |
| Lire un schéma et identifier des relations | Comprendre les rôles des machines et des routeurs |
| Distinguer un objet de son nom | Distinguer une adresse IP, un réseau et une interface |
| Suivre une suite d'étapes | Suivre le trajet d'un paquet |
| Compter et comparer des longueurs ou des coûts | Lire une table de routage et comparer des routes |

Pour **programmer** ensuite des algorithmes sur les graphes, il faut aussi connaître les listes ou dictionnaires, les boucles, les conditions et les fonctions. Ces outils ne sont pas nécessaires pour une première activité sur papier.

## 2. Les prérequis sur les réseaux

### Machines, commutateurs et routeurs

| Terme | Rôle dans un modèle simple |
| --- | --- |
| **Hôte** | Machine qui émet ou reçoit les données : ordinateur, serveur… |
| **Interface réseau** | Point de connexion d'une machine à un réseau, par exemple sa carte Ethernet |
| **Commutateur**, ou *switch* | Relie des équipements d'un même réseau local ; un commutateur Ethernet de niveau 2 utilise les adresses MAC pour transmettre les trames |
| **Routeur** | Relie des réseaux IP et choisit vers quelle interface transmettre un paquet |
| **Passerelle par défaut** | Routeur auquel un hôte confie les destinations pour lesquelles il n'a pas de route plus précise |

Une box domestique peut réunir plusieurs de ces fonctions. Il faut distinguer les **rôles**, même quand ils sont assurés par le même appareil.

### Adresses IPv4 et préfixes

Une adresse IPv4 comporte **32 bits**, habituellement écrits sous la forme de quatre nombres compris entre 0 et 255 : `192.168.1.10`. Une interface peut porter une adresse ; un routeur peut donc posséder plusieurs adresses, sur ses différentes interfaces. Le paquet contient notamment une adresse source et une adresse destination. [Référence : RFC 791, protocole IPv4](https://www.rfc-editor.org/rfc/rfc791).

La notation `192.168.1.10/24` précise que les **24 premiers bits** constituent le préfixe du réseau. Ici, cela correspond au masque `255.255.255.0` et au réseau `192.168.1.0/24`. Le masque sert à déterminer la partie réseau ; ce n'est pas l'adresse de la passerelle. [Référence : RFC 4632, notation des préfixes](https://datatracker.ietf.org/doc/html/rfc4632#section-3.1).

**Exemple, avec le même masque `/24` pour les trois machines :**

| Machine | Adresse | Réseau |
| --- | --- | --- |
| A | `192.168.1.10/24` | `192.168.1.0/24` |
| B | `192.168.1.20/24` | `192.168.1.0/24` |
| C | `192.168.2.20/24` | `192.168.2.0/24` |

A et B appartiennent au même sous-réseau. Dans le modèle habituel où elles sont reliées au même réseau local, elles communiquent sans passer par un routeur. Pour atteindre C, A doit utiliser un routeur.

**Attention :** comparer les trois premiers nombres ne fonctionne ici que parce que le préfixe est `/24`. Avec un autre préfixe, la séparation peut se situer ailleurs, y compris au milieu d'un octet.

### Paquets et acheminement

Les données sont transportées dans des **paquets**. À chaque étape, le routeur consulte l'adresse de destination et choisit un **prochain saut**, c'est-à-dire la prochaine étape vers cette destination. Il n'est pas nécessaire que chaque routeur stocke le trajet complet de chaque paquet.

Dans un modèle sans traduction d'adresses, l'adresse IP de destination reste celle de la machine finale : elle ne devient pas celle du prochain routeur. Le champ **TTL** diminue lors des passages par les routeurs ; le paquet est abandonné lorsqu'il expire, ce qui limite les boucles d'acheminement. [Référence : RFC 1812, acheminement IPv4](https://datatracker.ietf.org/doc/html/rfc1812#section-5.2).

## 3. Les prérequis sur les graphes

On note souvent un graphe `G = (S, A)`, où `S` est l'ensemble des **sommets** et `A` l'ensemble des **arêtes**. Pour un graphe orienté, on parle d'**arcs**.

| Notion | Définition | Exemple pour un réseau |
| --- | --- | --- |
| Sommet | Objet représenté | Un routeur |
| Arête | Relation entre deux sommets | Une liaison utilisable dans les deux sens |
| Voisins | Sommets reliés directement | Deux routeurs directement reliés |
| Chemin | Suite de sommets reliés successivement | `A → B → D` |
| Longueur d'un chemin | Nombre d'arêtes parcourues | `A → B → D` a une longueur de 2 |
| Poids | Valeur associée à une arête | Coût d'utilisation d'une liaison |
| Coût d'un chemin | Somme des poids de ses arêtes | Deux liaisons de coûts 3 et 5 donnent 8 |

Dans cette fiche, « chemin » désigne aussi un trajet dans un graphe non orienté ; certains cours emploient alors le mot **chaîne**.

Un graphe est **orienté** si les relations ont un sens. Un graphe non orienté est **connexe** si l'on peut relier toute paire de sommets par un chemin. Une liaison en panne peut rendre un sommet inaccessible, mais un autre chemin peut parfois prendre le relais.

### Passer du réseau au modèle

Pour commencer, on peut représenter uniquement les routeurs et les liaisons entre eux. Les ordinateurs et les réseaux locaux sont alors laissés de côté pour se concentrer sur le choix du trajet.

Il faut annoncer cette simplification : selon l'exercice, les sommets peuvent représenter des routeurs, des machines ou même des réseaux. **Le sens d'un sommet dépend du modèle choisi.**

## 4. Comprendre une table de routage

Une table de routage associe une destination, souvent un **préfixe réseau**, à un moyen de l'atteindre : directement par une interface ou via un prochain routeur.

**Exemple simplifié pour un routeur R1 :** R1 est relié à `192.168.1.0/24` et à `10.0.0.0/30`. Un routeur voisin R2 possède l'adresse `10.0.0.2` sur ce second réseau.

| Réseau destination | Prochain saut | Interface de sortie de R1 |
| --- | --- | --- |
| `192.168.1.0/24` | Directement connecté | `eth0` |
| `10.0.0.0/30` | Directement connecté | `eth1` |
| `192.168.2.0/24` | R2, à l'adresse `10.0.0.2` | `eth1` |

Un paquet destiné à `192.168.2.20` est donc transmis à R2. R2 poursuit ensuite l'acheminement avec sa propre table.

Quand plusieurs préfixes correspondent à la destination, le routeur retient le **plus spécifique**, celui dont le préfixe est le plus long. Une route par défaut `0.0.0.0/0` peut être utilisée si aucune route plus précise ne correspond. [Référence : RFC 1812, sélection de route](https://datatracker.ietf.org/doc/html/rfc1812#section-5.2.4.3).

## 5. Une progression possible pour l'enseignement

1. **Partir d'une situation concrète :** un ordinateur veut communiquer avec une machine située dans un autre réseau.
2. **Vérifier les prérequis :** faire identifier les hôtes, les réseaux, les adresses et la passerelle.
3. **Construire un graphe :** remplacer les routeurs par des sommets et les liaisons par des arêtes.
4. **Chercher plusieurs chemins :** montrer qu'une destination peut être accessible par différents trajets.
5. **Introduire un critère de choix :** moins de sauts ou plus faible coût total.
6. **Revenir aux tables :** traduire un chemin en décision locale, par exemple « depuis A, envoyer à B ».

Les protocoles RIP et OSPF peuvent ensuite servir à expliquer comment les routeurs construisent leurs informations de routage. Ils sont repris dans la [fiche de révision du 28 septembre](../28.09/note.md).

**Objectif observable :** l'élève sait justifier le prochain saut d'un paquet à partir d'un schéma et d'une table. Dire seulement « l'élève connaît les réseaux » est trop vague pour vérifier un apprentissage.

## 6. Vérifier sa compréhension

1. Faut-il connaître les adresses IP pour étudier un graphe de villes ?
2. Pourquoi une adresse IP seule ne suffit-elle pas à déterminer un sous-réseau ?
3. Quelle différence y a-t-il entre destination finale et prochain saut ?
4. Un chemin de deux arêtes est-il toujours moins coûteux qu'un chemin de trois arêtes ?

**Réponses :**

1. Non. Les graphes sont des modèles généraux ; l'adressage IP intervient dans leur application aux réseaux.
2. Il faut aussi connaître le préfixe ou le masque utilisé.
3. La destination finale est le destinataire du paquet ; le prochain saut est l'étape choisie pour s'en rapprocher.
4. Non. Deux arêtes de coût 10 donnent 20 ; trois arêtes de coût 1 donnent 3. Il faut préciser ce que signifie « le plus court ».
