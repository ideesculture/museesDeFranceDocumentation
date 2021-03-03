# 2. La structure de la base de données

Pour travailler efficacement avec le logiciel, il est impératif de comprendre les composants fondamentaux de la base de données de CollectiveAccess.

Même si CollectiveAccess offre une grande flexibilité dans la conception de votre modèle de données en définissant vos propres champs et propres relations et leurs contraintes, certains éléments structurants se retrouvent dans toute implémentation d’un profil.

## Les types d’enregistrement
CollectiveAccess définit 14 types d’enregistrements dans son modèle de données.

### Objet
L'objet est l'élément actif d'une collection. Il s’agit typiquement des éléments physiques ou numériques que vous gérez.

### Entité
Une entité correspond à une personne ou à un organisme, gérée dans une liste d'autorités, c'est à dire une liste autonome d’enregistrements.

Ainsi une personne ne sera créée qu'une fois et pourra ensuite être liée à d'autres enregistrements de tout type : objets créés ou possédés, lieux de naissance ou de vie, collection léguée, etc.

Les entités correspondent aux créateurs, artistes, dépositaires, éditeurs, transporteurs, assureurs et autres acteurs impliqués de quelque façon que ce soit à la collection.

### Lieu
Les lieux correspondent aux emplacements physiques et géographiques.

Les lieux sont intrinsèquement hiérarchisés et vous permettent ainsi de situer précisément les objets (ex : continent \> pays \> région \> ville \> adresse…).

Comme pour les entités, et ceci de manière globale dans CollectiveAccess, chaque enregistrement peut être lié à d'autres enregistrements, du même type ou d’un autre type.

### Occurrence
L’enregistrement « Occurrence » sert à désigner les **événements** (expositions,…), **procédures** (restauration, conservation, campagne de récolement,…) liés à plusieurs autres entrées dans la base de données. 

Chaque occurrence est décrite par des éléments de saisie et sera reliée à un ou plusieurs objets et autres enregistrements (entités, lieux…).

Une occurrence est un terme attribué à des éléments contextuels exigeant une saisie complexe, ne s’incarnant ni dans les objets, entités, lieux, collections ou localisations.

En règle générale, les occurrences sont utilisées pour saisir des événements historiques, expositions et bibliographies et servent de pivot pour l’enregistrement des fiches de récolement et pour toutes les procédures internes d’un établissement : restauration, procédure de conservation, organisation de convoiement, etc.

### Collection
Les collections représentent des collections physiques ou symboliques et regroupent des objets. 

Il vous est possible d’associer un objet à plusieurs collections simultanément.

### Lot
Un lot d’objets permet de rassembler la saisie des informations sur l’admission des objets enregistrés (donateur, date de réception, etc...) pour un don ou une acquisition de plusieurs objets.

Un objet ne peut faire partie que d’un seul lot.

### Ensemble
Un ensemble d’objets correspond à un groupement ordonné d'objets défini par les utilisateurs dans un but précis. 

Contrairement aux « collections », les ensembles sont des groupes appropriés à un rassemblement ponctuel d’enregistrements, qu’il soit propre à un des utilisateurs de CollectiveAccess ou partagé avec d’autres. 

Ainsi, on créera un ensemble pour préparer une exposition ou réaliser des traitements en lots pour un ensembles d’objets ; ou bien encore pour mettre de côté des entités à compléter.

### Elément d'un ensemble
L’enregistrement placé dans un ensemble est nommé « élément » ou « item ».

Il vous est possible d’attribuer aux éléments d’un ensemble des annotations, des légendes, des liens... ; ces métadonnées s’ajoutent aux métadonnées de l’objet.

### Représentation
Les représentations permettent de détailler et d’ajouter une saisie descriptive aux médias liés à un objet :

- légendes
- modalités d’accès
- droits de reproductions et restrictions éventuelles
- toute information nécessaire

Ces métadonnées descriptives enrichissent les médias associés aux objets (ou aux autres enregistrements.

Toutefois dans de nombreux cadres d’utilisation, on choisit de simplifier l’interface de Providence, et on ne complète que le champ « Représentation média » depuis l’objet.

### Emplacement de stockage
Les emplacements de stockage correspondent aux emplacements physiques où sont stockés les objets. 

Tout comme les lieux, ils sont gérés sous la forme d’une gestion hiérarchique, arborescente. Il vous est ainsi possible de décrire un ne hiérarchie d’emplacements afin de localiser un objet très précisément (bâtiment, salle, étagère, tiroir...). La saisie descriptive des emplacements comprend également les restrictions d'accès physique aux objets qui s'y trouvent, une carte, des coordonnées GPS afin de géo-localiser vos objets dans un espace.

### Liste
Une liste représente un groupe d'éléments organisé sous forme simple ou hiérarchisée. 

Dans CollectiveAccess, les listes sont utilisées dans les contextes suivants :

- listes déroulantes associées à un champ :
\*ex :  liste des types d’inscription, liste des modes d’acquisition »
-  vocabulaires contrôlés et associés à des objets, entités,
*ex : les thesaurus fournis par le Service des Musées de France ou toutes les listes contrôlées ajoutées selon les besoins : Domaine, Techniques et Matériaux, …*
- listes système, utilisées (et nécessaires) par l’interface de Providence et plus généralement pour la structure de la base.
*ex : types d’objets, types d’entités, relation objet-entât liée : auteur, artiste, producteur… *