# Tables principales et champs intrinsèques

CollectiveAccess est structuré autour de plusieurs **tables principales**, dont les éditeurs peuvent être activés (ou désactivés) selon les besoins du projet. Chaque table principale possède ses blocs intrinsèques et son propre jeu de blocs de labels préférés et non préférés. Des interfaces utilisateurs distinctes peuvent être configurées pour chaque table et, à l'intérieur, une même table peut avoir plusieurs interfaces utilisateurs restreintes par type.

Les éditeurs non pertinents pour votre système (vous ne cataloguez pas les lieux, par exemple) peuvent être désactivés dans le fichier de configuration `app.conf`, en réglant les directives `*_disable` ci-dessous sur une valeur non nulle. Voici à quoi cela ressemble dans `app.conf` :

```
# Editor "disable" switches
# -------------------
ca_objects_disable = 0
ca_entities_disable = 0
ca_places_disable = 0
ca_occurrences_disable = 0
ca_collections_disable = 0
ca_object_lots_disable = 0
ca_storage_locations_disable = 0
ca_loans_disable = 0
ca_movements_disable = 1
ca_tours_disable = 1
ca_tour_stops_disable = 1
ca_object_representations_disable = 1
```

## Objets (`ca_objects`)

Les fiches objet représentent les items ou actifs d'une collection, généralement les items physiques ou nativement numériques gérés. Chaque fiche objet a un « type » qui détermine quels champs lui sont pertinents. La liste des types disponibles dans votre système peut être personnalisée pour correspondre à vos exigences de catalogage.

!!! note
    `ca_objects.preferred_labels.name` est utilisé par les correspondances d'import et les modèles d'affichage pour référencer le champ intrinsèque `name` de la table `ca_object_labels`.

Principaux champs intrinsèques des objets :

| Nom | Code | Description | Obligatoire ? | Défaut |
|---|---|---|---|---|
| Identifiant | `idno` | L'identifiant de l'objet. Doit respecter la politique de numérotation configurée si `require_valid_id_number_for_ca_objects` est défini dans `app.conf`. Doit être unique si `allow_duplicate_id_number_for_ca_objects` n'est pas défini. | Selon politique de numérotation | |
| Type | `type_id` | Une valeur de la liste `object_types` indiquant le type de l'enregistrement. Stocké comme `item_id` numérique interne. Lors d'un import ou via l'API, l'identifiant de l'élément peut être utilisé. | | |
| Parent | `parent_id` | Référence à l'enregistrement parent. Nul si aucun parent n'est défini. | Non | null |
| Accès | `access` | Détermine la visibilité dans les applications publiques comme Pawtucket. Valeurs définies dans la liste `access_statuses`. Par convention, « 0 » = privé et « 1 » = public (modifiable dans `app.conf`). | Oui | 0 |
| Statut | `status` | Statut général de l'enregistrement dans le flux de catalogage. Valeurs définies dans `workflow_statuses`. Purement informatif, sans impact fonctionnel. | Oui | 0 |
| Lot | `lot_id` | Référence au lot (`ca_object_lots`) dont l'objet fait partie. Un objet ne peut appartenir qu'à un seul lot. | Non | |
| Source | `source_id` | Une valeur de la liste `object_sources` indiquant la source d'origine de l'objet. | Non | |
| Sorti de l'inventaire ? | `is_deaccessioned` | Indicateur de sortie d'inventaire : 1 si sorti, 0 (défaut) sinon. | Oui | 0 |
| Date de sortie d'inventaire | `deaccession_date` | Date de sortie d'inventaire (plage de dates historique). | Non | |
| Date de cession | `deaccession_disposal_date` | Date de cession de l'objet, généralement postérieure à la sortie d'inventaire. | Non | |
| Notes de sortie d'inventaire | `deaccession_notes` | Notes sur le processus de sortie d'inventaire (65535 caractères max.). | Non | |
| Type de sortie d'inventaire | `deaccession_type_id` | Une valeur de `object_deaccession_types` (ex. « Vendu », « Détruit », « Transféré »). | Non | |
| Type d'acquisition | `acquisition_type_id` | Une valeur de `object_acq_types` indiquant le mode d'acquisition de l'objet. | Non | |
| Statut d'acquisition | `item_status_id` | Une valeur de `object_statuses` (ex. « acquis », « acquisition en attente », « item non acquis »). | Non | |
| Étendue | `extent` | L'étendue numérique. Nombre entier positif. | Oui | 0 |
| Unités d'étendue | `extent_units` | Unités de l'étendue, en texte. | Oui | |
| Statut de circulation | `circulation_status_id` | Une valeur de `object_circulation_statuses` (statut de prêt/retour bibliothèque). | Non | |
| Emplacement d'origine | `home_location_value` | L'emplacement d'origine de l'objet, mis en forme selon `home_location_display_template` d'`app.conf`. | Non | |

!!! note
    Les champs `submission_*` (utilisateur, groupe, statut, formulaire) et `view_count` concernent les enregistrements soumis via le formulaire « contribuer » de Pawtucket et le nombre de consultations sur le front-end.

## Lots d'objets (`ca_object_lots`)

Les lots enregistrent l'acquisition d'un ou plusieurs objets. Ils sont couramment utilisés par les institutions qui peuvent acquérir plus d'un item unique par acquisition. Les informations de régie, comme l'acte de don, peuvent être enregistrées dans une fiche lot, tandis que le catalogage de chaque objet acquis reste au niveau de l'objet.

## Entités (`ca_entities`)

Les fiches entité représentent des personnes et des organisations précises. Des relations peuvent être créées entre les fiches entité et objet (ou tout autre enregistrement de toute autre table), avec des types de relation entièrement personnalisables. Par exemple, une fiche entité d'un individu pourrait être liée à une fiche objet comme créateur de l'objet, ou comme photographe, donateur, éditeur, interprète, etc.

!!! note
    `ca_entities.preferred_labels.displayname` est utilisé par les correspondances d'import et les modèles d'affichage pour référencer le champ intrinsèque `displayname` de la table `ca_entity_labels`.

Principaux champs intrinsèques des entités :

| Nom | Code | Description | Obligatoire ? | Défaut |
|---|---|---|---|---|
| Identifiant | `idno` | L'identifiant de l'entité. Soumis à la politique de numérotation et aux contraintes d'unicité configurées dans `app.conf`. | Selon politique de numérotation | |
| Type | `type_id` | Une valeur de la liste `entity_types` indiquant le type de l'enregistrement. | Oui | null |
| Parent | `parent_id` | Référence à l'enregistrement parent. Nul si aucun parent. | Non | null |
| Accès | `access` | Visibilité dans les applications publiques. Valeurs dans `access_statuses` (« 0 » privé, « 1 » public par convention). | Oui | 0 |
| Statut | `status` | Statut dans le flux de catalogage. Valeurs dans `workflow_statuses`. Purement informatif. | Oui | 0 |
| Période de vie | `lifespan` | Les dates de vie de l'entité (plage de dates historique). | Non | |
| Source | `source_id` | Une valeur de `entity_sources` indiquant la source d'origine de l'entité. | Non | |

## Lieux (`ca_places`)

Les fiches lieu représentent des localisations physiques, géographiques ou autres. Les lieux sont par nature hiérarchiques, permettant d'imbriquer des fiches plus précises au sein de fiches plus larges. Comme les entités, les lieux peuvent être liés à des enregistrements d'autres tables. Ils servent généralement à modéliser des autorités de localisation propres à votre système. Pour le catalogage des noms de lieux géographiques courants, envisagez la prise en charge intégrée de CollectiveAccess pour GoogleMaps, OpenStreetMap, GeoNames et/ou le Getty Thesaurus of Geographic Names (TGN).

## Occurrences (`ca_occurrences`)

Les occurrences représentent des concepts temporels comme des événements, expositions, productions ou citations.

## Collections (`ca_collections`)

Les collections représentent des regroupements significatifs d'objets. Elles peuvent désigner des collections physiques, des collections symboliques d'items associés par un critère, ou tout autre regroupement. Les fiches collection servent souvent à gérer le traitement archivistique formel et la création d'instruments de recherche, en configurant les fiches pour qu'elles respectent la norme de contenu DACS (*Describing Archives*).

## Emplacements de stockage (`ca_storage_locations`)

Les fiches d'emplacement de stockage représentent les localisations physiques où les objets peuvent se trouver, être exposés ou stockés. Comme les fiches lieu, les emplacements de stockage sont hiérarchiques et peuvent être imbriqués pour noter la localisation à divers niveaux de précision (bâtiment, salle, armoire, tiroir, etc.). Comme les autres tables principales, chaque emplacement peut comporter un catalogage arbitrairement riche : restrictions d'accès, coordonnées géographiques, mots-clés et autres informations.

## Prêts (`ca_loans`)

Les fiches prêt enregistrent les détails des prêts entrants et sortants d'objets. Comme toutes les autres, elles sont entièrement personnalisables et peuvent servir à suivre tous les aspects d'un prêt : dates, transport, informations d'assurance.

## Mouvements (`ca_movements`)

Pour les besoins de suivi de localisation plus complexes, les fiches mouvement permettent d'enregistrer dans le détail le déplacement des objets entre emplacements de stockage, pendant un prêt ou une exposition. Intégrées à une politique de suivi de localisation ou d'historique d'utilisation, elles fournissent un enregistrement robuste de chaque événement de déplacement dans l'histoire d'un objet.

## Représentations d'objet (`ca_object_representations`)

Les représentations capturent les médias numériques représentatifs (images, vidéo, audio, PDF) des objets. Une fiche représentation ne contient généralement qu'un fichier média, mais peut accueillir un catalogage supplémentaire propre au fichier (et non à l'objet qu'il représente) : légendes, crédits, informations d'accès, droits et restrictions de reproduction.

## Visites (`ca_tours`) et étapes de visite (`ca_tour_stops`)

Les fiches visite capturent des informations sur les visites, sur site ou en ligne, d'objets, de lieux, de collections ou de tout autre enregistrement. Chaque fiche visite comporte un nombre quelconque d'« étapes » ordonnées. Chaque étape contient des métadonnées (texte descriptif, coordonnées géographiques, etc.) ainsi que des relations vers les objets, entités et autres enregistrements pertinents.

## Tables de labels

Les labels sont les noms ou titres des enregistrements. Toutes les tables principales ont des tables de labels associées. Les labels existent en deux variétés : préférés et non préférés. Chaque enregistrement a un, et un seul, label préféré, utilisé comme titre d'affichage par défaut. Un enregistrement peut avoir un nombre quelconque de labels non préférés, considérés comme des titres alternatifs et utilisables dans les recherches. Les labels sont toujours présents et n'ont pas besoin d'être configurés pour exister.

La notation abrégée suivante est couramment utilisée pour référencer les labels préférés : `<nom de table>.preferred_labels.<champ nom de la table de labels>`. Par exemple, ceci afficherait le label préféré d'un objet :

```
ca_objects.preferred_labels.name
```

!!! note
    `<nom de table>.preferred_labels.<nom de l'intrinsèque>` est utilisé par les correspondances d'import et les modèles d'affichage pour référencer le champ intrinsèque _name_ des labels préférés. La construction `<nom de table>.preferred_labels` est simplement un alias de la table de labels, filtré pour ne renvoyer que les entrées dont `is_preferred` est défini. Par exemple, `ca_objects.preferred_labels.name` et `ca_object_labels.name` désignent la même chose, sauf que la version `ca_object_labels.name` renvoie _tous_ les labels, tandis que `ca_objects.preferred_labels.name` ne renvoie que ceux marqués comme préférés. De même, `<nom de table>.nonpreferred_labels.<nom de l'intrinsèque>` renvoie toutes les entrées _non_ marquées comme préférées.

Correspondance table principale → table de labels :

| Table principale | Table de labels |
|---|---|
| `ca_objects` | `ca_object_labels` |
| `ca_object_lots` | `ca_object_lot_labels` |
| `ca_entities` | `ca_entity_labels` |
| `ca_places` | `ca_place_labels` |
| `ca_occurrences` | `ca_occurrence_labels` |
| `ca_collections` | `ca_collection_labels` |
| `ca_storage_locations` | `ca_storage_location_labels` |
| `ca_loans` | `ca_loan_labels` |
| `ca_movements` | `ca_movement_labels` |
| `ca_object_representations` | `ca_object_representation_labels` |
| `ca_tours` | `ca_tour_labels` |
| `ca_tour_stops` | `ca_tour_stop_labels` |

### Champs disponibles pour toutes les tables de labels

| Nom | Code | Description |
|---|---|---|
| Préféré ? | `is_preferred` | Un label préféré est le seul « vrai » titre ou nom d'un item — celui à utiliser pour le désigner — servant à l'affichage. Il ne peut y avoir qu'un seul label préféré par item et par locale (en cataloguant en trois langues, vous pouvez avoir jusqu'à trois labels préférés). Les labels non préférés sont des noms alternatifs qui améliorent la recherche ou préservent l'identité ; ils peuvent se répéter sans limite, prennent des locales et optionnellement des valeurs de type. |
| Tri du nom | `name_sort` | Version du label générée automatiquement, utilisée pour le tri. |
| Type | `type_id` | |
| Source | `source_info` | |
| Locale | `locale_id` | Locale du label. |

!!! note
    `ca_tour_labels` et `ca_tour_stop_labels` ne contiennent pas `type`, `source_info` ni `is_preferred`.

### Champs « nom » des labels

Les champs de nom des tables de labels peuvent différer d'une table à l'autre.

Pour les labels d'objet, lot d'objets, lieu, occurrence, collection, emplacement de stockage, prêt, mouvement, représentation d'objet, visite et étape de visite, le champ est :

| Nom | Code | Description |
|---|---|---|
| Nom | `name` | Nom de l'enregistrement, utilisé pour l'affichage. |

Pour les **labels d'entité** (`ca_entity_labels`) :

| Nom | Code | Description |
|---|---|---|
| Nom d'affichage | `displayname` | Nom complet de l'entité, utilisé pour l'affichage. |
| Prénom | `forename` | Prénom de l'entité. |
| Autres prénoms | `other_forename` | Prénoms alternatifs. |
| Deuxième prénom | `middlename` | Deuxième prénom de l'entité. |
| Nom de famille | `surname` | Nom de famille de l'entité. |
| Préfixe | `prefix` | Préfixe de l'entité. |
| Suffixe | `suffix` | Suffixe de l'entité. |

## Intrinsèques spéciaux

Des intrinsèques supplémentaires donnent accès aux informations du journal des modifications, à l'origine et au suivi de l'historique. Ils sont potentiellement disponibles pour de nombreuses tables principales, voire toutes.

| Code | Description | S'applique à | Exemples |
|---|---|---|---|
| `created` | Date/heure de création de l'enregistrement, formatée selon les réglages système. Sous-champs optionnels : `user`, `fname`, `lname`, `email` (utilisateur créateur) et `timestamp` (horodatage Unix). | Tout enregistrement | `ca_objects.created`, `ca_objects.created.timestamp`, `ca_objects.created.email` |
| `lastModified` | Date/heure de dernière modification, formatée selon les réglages système. Mêmes sous-champs que `created`, relatifs au dernier modificateur. | Tout enregistrement | `ca_objects.lastModified`, `ca_objects.lastModified.timestamp`, `ca_objects.lastModified.email` |
| `_guid` | Un identifiant unique global (GUID) de l'enregistrement, identique à celui utilisé pour suivre les enregistrements dans les systèmes répliqués. (Depuis la version 1.8) | Tout enregistrement | `ca_objects.guid` |
| `history_tracking_current_value` | Valeur actuelle d'une politique de suivi de l'historique. La politique par défaut est utilisée sauf surcharge via l'option `policy`. | Tout enregistrement ayant une politique de valeur actuelle | `ca_objects.history_tracking_current_value`, `…%policy=provenance` |
| `history_tracking_current_date` | Date de la valeur actuelle d'une politique de suivi. Politique par défaut sauf surcharge via `policy`. | Idem | `ca_objects.history_tracking_current_date`, `…%policy=provenance` |
| `history_tracking_current_contents` | Valeurs de tous les enregistrements qui utilisent cet enregistrement comme valeur actuelle. | Tout enregistrement utilisé par au moins une politique | `ca_storage_locations.history_tracking_current_contents`, `…%policy=current_location` |
| `submitted_by_user` | Nom et e-mail de l'utilisateur ayant soumis l'enregistrement via le formulaire « contribuer » de Pawtucket. Personnalisable via `display_template`. | Objets, entités, lieux, occurrences, collections, lots, prêts, mouvements, emplacements, représentations | `ca_objects.submitted_by_user` |
| `submission_group` | Le groupe de l'utilisateur au moment de la soumission via le formulaire « contribuer ». Personnalisable via `display_template`. | Idem | `ca_objects.submission_group` |

!!! info "Référence exhaustive"
    Les champs intrinsèques détaillés des tables non couvertes ci-dessus (lots, lieux, occurrences, collections, emplacements, prêts, mouvements, représentations, visites) suivent le même schéma. La référence complète est dans la [documentation officielle Providence](https://providence.readthedocs.io/en/latest/) et dans la section [Schéma de la base de données](schema_introduction.md).

!!! info "Source"
    Traduction de la documentation officielle [CollectiveAccess / Providence](https://providence.readthedocs.io/en/latest/), section *Data Modelling — Primary Tables*. Terminologie alignée sur le fichier de localisation `fr_FR` de l'application.
