# Introduction aux données dans CollectiveAccess

## Tables principales et enregistrements

CollectiveAccess est structuré autour de plusieurs **tables principales** d'éléments de métadonnées : Objets, Entités, Collections, et d'autres. Chaque table principale possède ses blocs intrinsèques et son propre jeu de blocs de labels préférés et non préférés.

En savoir plus : [Tables principales](modelisation_tables_principales.md).

## Blocs (*bundles*)

« Bloc » est un terme générique désignant les diverses structures de CollectiveAccess servant à stocker le contenu catalogué. Il existe quatre types distincts de blocs, chacun avec ses caractéristiques et usages propres : les **labels**, les **intrinsèques**, les **éléments de métadonnées** et les **relations**. Les enregistrements ne sont que des assemblages de divers blocs, choisis pour répondre à des besoins de représentation précis.

### Labels

Les labels servent à stocker les noms ou titres des enregistrements. Ils existent en deux variétés : préférés et non préférés. Chaque enregistrement a un, et un seul, label préféré qui représente le « nom » actuel de l'enregistrement et sert de titre d'affichage par défaut.

Les enregistrements peuvent avoir un nombre quelconque de labels non préférés. Ceux-ci servent généralement à enregistrer des noms/titres alternatifs, utilisables dans les recherches et affichables au besoin.

Les labels préférés et non préférés sont toujours disponibles pour tous les enregistrements de CollectiveAccess. Aucune configuration particulière n'est requise. Notez que (à quelques exceptions près) chaque enregistrement de CollectiveAccess **doit** avoir un label préféré. Des options de configuration permettent d'imposer l'unicité des labels dans un système, de distinguer différents types de labels non préférés (exigence de certaines normes de représentation des connaissances), et plus encore.

En savoir plus : [Labels](modelisation_tables_principales.md#tables-de-labels).

### Intrinsèques

Les intrinsèques sont des champs intégrés présents dans tous les systèmes CollectiveAccess. Comme les labels, ils sont toujours disponibles et ne nécessitent pas de configuration particulière. Les intrinsèques sont des valeurs simples, non répétables, qui existent généralement pour prendre en charge une fonctionnalité précise ou, plus rarement, pour des raisons historiques. Ils ne peuvent pas être retirés de CollectiveAccess, mais peuvent dans la plupart des cas être masqués s'ils ne sont pas nécessaires.

Parmi les intrinsèques d'usage courant : `idno` (identifiant de l'enregistrement), `type_id` (type d'enregistrement), `access` (visibilité sur le site public) et `status` (statut de l'enregistrement dans le flux de travail). Les descriptions de tous les champs intrinsèques disponibles figurent dans la documentation des [tables principales](modelisation_tables_principales.md).

### Éléments de métadonnées

Les éléments de métadonnées sont des champs de données configurables liés aux divers enregistrements de votre schéma de données. Ils peuvent accepter une gamme riche et variée de types de données, se répéter, prendre en charge des valeurs multilingues, et se composer en champs complexes à plusieurs valeurs grâce aux éléments conteneurs. L'essentiel du schéma de données d'un système typique est implémenté à l'aide d'éléments de métadonnées pour construire des structures de données propres à l'installation.

En savoir plus : [Métadonnées](modelisation_metadonnees.md).

### Relations

Les relations sont des liens bidirectionnels entre des paires d'enregistrements. Elles peuvent être créées entre des enregistrements de n'importe quelle table principale, sans restriction. Toute relation comporte une référence à un **type de relation** — un spécificateur configurable qui distingue les différentes natures de relations possibles. Les types de relation entre objets et entités pourraient inclure, par exemple, « créateur », « donateur » et « sujet ».

Un nombre quelconque de relations peut être créé entre une paire d'enregistrements, et chaque relation peut optionnellement intégrer des éléments de métadonnées supplémentaires (voir [Données interstitielles](interstitiel.md)). Les relations prennent aussi en charge quelques intrinsèques, mais ne prennent pas de labels.

## Profils d'installation

Les profils d'installation sont les documents XML qui créent votre modèle de données et configurent votre base. Toute instance CollectiveAccess doit avoir un profil d'installation. De nombreuses options sont préchargées, mais il faut généralement en personnaliser un selon vos besoins.

!!! info "Source"
    Traduction de la documentation officielle [CollectiveAccess / Providence](https://providence.readthedocs.io/en/latest/), section *Data Modelling — Introduction to Data*. Terminologie alignée sur le fichier de localisation `fr_FR` de l'application.
