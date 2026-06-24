# P7 — Concevez et analysez une base de données NoSQL

## Présentation du projet

Ce projet a été réalisé dans le cadre du parcours **Data Engineer** d’OpenClassrooms.

L’objectif est de restaurer, analyser et concevoir une base de données NoSQL avec **MongoDB** pour l’association fictive **NosCités**, qui surveille les plateformes de locations courte durée afin d’évaluer leur impact sur l’offre de logements en France.

Le projet se concentre principalement sur les données de locations courte durée à **Paris pendant l’été 2024**, dans le contexte des Jeux Olympiques, puis étend la réflexion à une architecture multi-sites entre **Paris** et **Lyon**.

---

## Contexte métier

L’association NosCités souhaite produire des analyses fiables sur l’impact des plateformes de location courte durée sur le marché du logement.

À la suite d’un crash de la base de données de Paris, une sauvegarde doit être restaurée, vérifiée et analysée rapidement afin de confirmer que les données sont cohérentes avec les besoins de l’équipe parisienne.

Le projet répond donc à trois objectifs principaux :

* restaurer une base de données MongoDB à partir d’une sauvegarde ;
* analyser l’intégrité et la cohérence des données avec des requêtes MongoDB et Python ;
* proposer une architecture NoSQL plus robuste avec réplication et distribution des données.

---

## Structure du dépôt

```text
p7-concevez-analysez-base-donnees-nosql/
├── README.md
├── presentation/
│   └── MotasemAbualqumboz_Concevez_et_analysez_une_base_de_donnees_NoSQL_090525.pptx
└── notebooks/
    └── polars.ipynb
```

---

## Livrable principal

Le livrable officiel de ce projet est le support de présentation PowerPoint.

Il contient :

* le contexte du projet ;
* les bénéfices du NoSQL dans ce cas d’usage ;
* la restauration et l’exploration de la base MongoDB ;
* les premières requêtes MongoDB ;
* les analyses statistiques simples et complexes ;
* la démarche de connexion à un outil de BI ;
* la stratégie de réplication avec MongoDB Replica Set ;
* la stratégie de distribution avec MongoDB Sharding ;
* la vérification de la distribution Paris/Lyon.

Le notebook `polars.ipynb` est fourni comme support complémentaire pour la partie d’analyse avancée réalisée avec Python, PyMongo et Polars.

---

## Partie 1 — Restauration et exploration de la base MongoDB

La première partie du projet consiste à restaurer les données de locations courte durée de Paris dans MongoDB.

Les principales tâches réalisées sont :

* importation des données dans MongoDB ;
* observation de la structure des documents ;
* analyse des types de données ;
* premières requêtes avec MongoDB ;
* comptage du nombre total de documents ;
* comptage des logements avec disponibilité.

Résultats principaux :

* 95 885 documents importés pour Paris ;
* 76 747 logements avec `availability_365 > 0`.

---

## Pourquoi MongoDB / NoSQL ?

MongoDB est adapté à ce projet car les données de locations courte durée sont semi-structurées et peuvent contenir des champs variés selon les annonces.

Les bénéfices principaux sont :

* schéma flexible ;
* gestion native des documents imbriqués ;
* absence de jointures complexes pour les structures semi-structurées ;
* requêtes efficaces sur des champs imbriqués ;
* scalabilité horizontale avec le sharding ;
* haute disponibilité avec les replica sets ;
* bonne intégration avec des outils d’analyse et de BI.

---

## Partie 2 — Analyse de la base de données NoSQL

La deuxième partie du projet consiste à produire des statistiques et indicateurs pour vérifier la cohérence des données avec l’équipe parisienne.

Les requêtes MongoDB simples ont permis de calculer :

* le nombre d’annonces par type de logement ;
* les 5 annonces avec le plus grand nombre d’évaluations ;
* le nombre total d’hôtes différents ;
* le nombre et la proportion de locations réservables instantanément ;
* les hôtes possédant plus de 100 annonces ;
* le nombre et la proportion de super-hôtes.

Résultats principaux :

* 71 979 hôtes différents ;
* 24 hôtes avec plus de 100 annonces ;
* environ 14 % des hôtes sont des super-hôtes ;
* environ 23 % des annonces sont réservables instantanément.

---

## Analyses avancées avec PyMongo et Polars

Certaines analyses plus complexes ont été réalisées avec Python, PyMongo et Polars.

Le notebook `polars.ipynb` sert de support pour cette partie.

Les analyses incluent :

* taux de réservation moyen par mois par type de logement ;
* médiane du nombre d’avis pour tous les logements ;
* médiane du nombre d’avis par catégorie d’hôte ;
* densité de logements par quartier de Paris ;
* identification des quartiers avec le plus fort taux de réservation mensuel.

Polars a été utilisé pour faciliter les calculs statistiques et les agrégations avancées en mémoire.

---

## Connexion à un outil de Business Intelligence

Le projet inclut également une démarche de mise à disposition des données via un outil de BI.

L’objectif était de permettre à l’équipe parisienne de visualiser les résultats de l’analyse et de continuer ses travaux plus facilement.

La présentation montre la connexion entre MongoDB et Tableau, ainsi qu’un exemple de tableau de bord.

---

## Partie 3 — Conception d’une architecture NoSQL robuste

La troisième partie du projet consiste à proposer une architecture plus résiliente et scalable.

Cette architecture répond à deux enjeux :

* éviter une nouvelle perte d’accès aux données en cas de panne ;
* améliorer les performances de requêtes pour les équipes locales de Paris et Lyon.

---

## Réplication avec MongoDB Replica Set

Une stratégie de réplication a été conçue pour garantir une meilleure disponibilité des données.

La logique retenue repose sur :

* un nœud primaire ;
* un nœud secondaire ;
* un arbitre ;
* un mécanisme de basculement automatique en cas de panne.

La réplication permet :

* d’améliorer la tolérance aux pannes ;
* de garantir une copie des données sur plusieurs nœuds ;
* de maintenir l’accès aux données en cas d’incident sur le serveur primaire.

---

## Distribution avec MongoDB Sharding

Une stratégie de sharding a été proposée afin de distribuer les données entre Paris et Lyon.

Les données de Paris et Lyon sont réunies dans une seule collection `listings`, avec un champ `city` permettant de distinguer l’origine géographique des documents.

La clé de sharding utilisée est :

```text
city
```

La stratégie de distribution repose sur une logique géographique :

* les documents de Paris sont placés sur le shard Paris ;
* les documents de Lyon sont placés sur le shard Lyon.

Cette approche permet d’optimiser les performances des requêtes locales pour chaque équipe.

Résultat de distribution :

* 95 885 documents sur le shard Paris ;
* 9 973 documents sur le shard Lyon ;
* 0 document orphelin.

---

## Technologies utilisées

* MongoDB
* Mongosh
* MongoDB Compass
* MongoDB Replica Set
* MongoDB Sharding
* PyMongo
* Polars
* Python
* Tableau
* PowerPoint

---

## Compétences démontrées

Ce projet démontre les compétences suivantes :

* restauration d’une base MongoDB ;
* compréhension des bénéfices du NoSQL ;
* analyse de documents semi-structurés ;
* écriture de requêtes MongoDB simples et complexes ;
* utilisation de Python, PyMongo et Polars pour l’analyse avancée ;
* connexion d’une base MongoDB à un outil de BI ;
* conception d’une stratégie de réplication ;
* conception d’une stratégie de sharding ;
* réflexion sur la haute disponibilité, la scalabilité et la résilience d’une architecture NoSQL.

---

## Remarque

Les fichiers de données brutes ne sont pas inclus dans ce dépôt.

Le livrable officiel du projet est le support de présentation. Le notebook Polars est ajouté comme élément complémentaire pour documenter une partie des calculs analytiques.

---

## Auteur

Motasem Abualqumboz

Data Engineer
