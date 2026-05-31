# Gestion des données dans CollectiveAccess

Traduit depuis manual.collectiveaccess.org par Gautier Michelin pour IdéesCulture (mai 2024)

## Introduction à la gestion des données dans CollectiveAccess

**Tables et enregistrements primaires**
CollectiveAccess est structuré autour de plusieurs tables primaires d'éléments de métadonnées, tels que les objets, les entités, les collections, etc. Chaque table primaire possède des données intrinsèques et son propre ensemble de labels préférés et non préférés (titre ou nom par exemple).

**Bundles**
Un bundle est un terme de haut niveau qui désigne les différentes structures de CollectiveAccess utilisées pour stocker le contenu catalogué. Il existe quatre types distincts de bundles, chacun ayant son propre ensemble de caractéristiques et d'utilisations : les labels, les métadonnées intrinsèques, les éléments de métadonnées et les relations. Les enregistrements (entités, objets, lieux, emplacements de stockages, représentations, …) sont simplement des assemblages de différentes bundles, choisis pour répondre à des exigences de description spécifiques.

**Labels**
Les labels sont utilisés pour stocker les noms ou les titres des documents. Il existe deux types de labels : les labels préférés et les labels non préférés. Chaque enregistrement possède un, et un seul, label préféré qui représente le "nom" actuel de l'enregistrement et qui est utilisé comme titre d'affichage par défaut.

Les enregistrements peuvent avoir un nombre quelconque de labels non préférés. Les labels non préférés sont généralement utilisées pour enregistrer des noms/titres alternatifs, qui peuvent être utilisés dans les recherches et éventuellement affichés.

Les labels préférés et non préférés sont toujours disponibles pour tous les enregistrements dans CollectiveAccess. Aucune configuration particulière n'est requise. Notez que (à quelques exceptions près) chaque enregistrement dans CollectiveAccess doit avoir un label préféré. Des options de configuration peuvent être définies pour gérer l'unicité des labels, pour distinguer les différents types de labels non préférés (une exigence de certains standards de descriptions des métadonnées) et plus encore.

**Métadonnées Intrinsèques**
Les éléments intrinsèques sont des champs intégraux présents dans tous les systèmes CollectiveAccess. Tout comme les labels, les métadonnées intrinsèques sont toujours disponibles et ne nécessitent pas de configuration particulière. Il s'agit de valeurs simples, qui ne se répètent pas et qui existent généralement pour prendre en charge une fonctionnalité spécifique ou, plus rarement, pour des raisons historiques. Elles ne peuvent pas être supprimées de CollectiveAccess, mais dans la plupart des cas, elles peuvent être masquées si elles ne sont pas nécessaires.

Les champs intrinsèques couramment utilisés sont **idno** (identifiant de l'enregistrement), **type\_id** (type d'enregistrement), **access** (visibilité sur le site web public) et **status** (statut du flux de travail de l'enregistrement). Les descriptions de tous les champs intrinsèques disponibles se trouvent dans la documentation de la table primaire.

**Éléments de métadonnées**
Les éléments de métadonnées sont des champs de données configurables liés aux différents enregistrements de votre schéma de données. Les éléments de métadonnées peuvent accepter une gamme riche et variée de types de données, peuvent se répéter, peuvent prendre en charge des valeurs multilingues et peuvent être composés en champs complexes à valeurs multiples à l'aide d'éléments conteneurs. La majeure partie du schéma de données d'un système typique sera mise en œuvre à l'aide d'éléments de métadonnées pour construire des structures de données spécifiques à l'installation.

**Relations**
Les relations sont des liens bidirectionnels entre des paires d'enregistrements. Ils peuvent être créés entre des enregistrements de n'importe quelle table primaire sans restriction. Tous les liens comprennent des références à des types de relations - des descripteurs configurables qui distinguent les différents types de liens possibles. Les types de relations entre les enregistrements d'objets et d'entités peuvent inclure, par exemple, "créateur", "donateur" et "sujet".

Il est possible de créer un nombre illimité de relations entre deux enregistrements, et chaque relation peut éventuellement intégrer des éléments de métadonnées supplémentaires. Les relations prennent également en charge une poignée d'éléments intrinsèques, mais n'acceptent pas de label.

**Profils d'installation**
Les profils d'installation sont les documents XML qui créent votre modèle de données et configurent votre base de données. Chaque instance de CollectiveAccess doit disposer d'un profil d'installation. De nombreuses options sont préchargées, mais vous devez généralement en personnaliser un en fonction de vos besoins.

## Tables primaires et champs intrinsèques
CollectiveAccess est structuré autour de plusieurs tables primaires, avec des éditeurs qui peuvent être activés (ou désactivés) en fonction des exigences du projet. Chaque tableau primaire possède des lots intrinsèques et son propre ensemble de lots d'étiquettes préférées et non préférées. Des interfaces utilisateur distinctes peuvent être configurées pour chaque table et, au sein de celles-ci, une même table peut avoir plusieurs interfaces utilisateur restreintes par type.

Les éditeurs qui ne sont pas pertinents pour votre système (vous ne cataloguez pas les lieux par exemple) peuvent être désactivés dans le fichier de configuration app.conf, en définissant les différentes directives \*\_disable ci-dessous à une valeur non nulle.

Voici à quoi ressemble le fichier app.conf :

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

### Objets (ca\_objects)
Les enregistrements d'objets représentent des éléments ou des biens d'une collection, généralement des éléments physiques ou numériques gérés. Chaque enregistrement d'objet a un "type" qui détermine les champs qui lui sont pertinents. La liste des types disponibles dans votre système peut être personnalisée pour répondre à vos besoins spécifiques en matière de catalogage.

### Lots d'objets (ca\_object\_lots)
Les lots enregistrent l'adhésion ou l'acquisition d'un ou plusieurs objets. Les lots sont couramment utilisés par les institutions de collection qui peuvent acquérir plus d'un objet unique par acquisition. Les informations relatives à l'enregistrement, telles que l'acte de donation, peuvent être enregistrées dans une fiche de lot, tandis que le catalogage de chaque objet acquis reste au niveau de l'objet.

### Entités (ca\_entities)
Les enregistrements d'entités représentent des personnes et des organisations spécifiques. Des relations peuvent être créées entre les enregistrements d'entités et d'objets (ou tout autre enregistrement dans n'importe quelle autre table) avec des types de relations entièrement personnalisables. Par exemple, un enregistrement d'entité pour une personne peut être lié à un enregistrement d'objet en tant que créateur de l'objet, ou en tant que photographe, donateur, éditeur, artiste, etc.

### Lieux (ca\_places)
Les enregistrements de lieux représentent des emplacements physiques, géographiques ou autres. Les lieux sont intrinsèquement hiérarchiques, ce qui permet d'imbriquer des enregistrements de lieux plus spécifiques dans des enregistrements plus généraux. Comme pour les entités, les lieux peuvent être liés à des enregistrements d'autres tables. Les lieux sont généralement utilisés pour modéliser les autorités de localisation spécifiques à votre système. Pour le catalogage des noms de lieux géographiques courants, pensez à utiliser le support intégré de CollectiveAccess pour GoogleMaps, OpenStreetMap, GeoNames et/ou le Getty Thesaurus of Geographic Names (TGN).

### Occurrences (ca\_occurrences)
Les occurrences sont utilisées pour représenter des concepts temporels tels que des événements, des expositions, des productions ou des citations.

### Collections (ca\_collections)
Les collections représentent des regroupements significatifs d'objets. Elles peuvent faire référence à des collections physiques, à des collections symboliques d'éléments associés par certains critères, ou à tout autre regroupement. Les notices de collection sont souvent utilisées pour gérer le traitement formel des archives et la création d'instruments de recherche, en configurant les notices de manière à ce qu'elles soient conformes à la norme de contenu Describing Archives (DACS).

### Emplacements de stockage (ca\_storage\_locations)
Les enregistrements relatifs aux lieux de stockage représentent les emplacements physiques où les objets peuvent être situés, exposés ou stockés. Comme les enregistrements de lieux, les emplacements de stockage sont hiérarchiques et peuvent être imbriqués pour permettre la notation de l'emplacement à différents niveaux de spécificité (bâtiment, pièce, armoire, tiroir, etc.). Comme pour les autres tables primaires, chaque lieu de stockage peut faire l'objet d'un catalogage arbitrairement riche, comprenant des restrictions d'accès, des coordonnées géographiques, des mots-clés et d'autres informations.

### Prêts (ca\_loans)
Les fiches de prêt enregistrent les détails des prêts d'objets, qu'ils soient entrants ou sortants. Les enregistrements de prêts, comme ceux de toutes les autres tables, sont entièrement personnalisables et peuvent être utilisés pour suivre tous les aspects d'un prêt, y compris les dates, l'expédition et les informations relatives à l'assurance.

### Mouvements (ca\_movements)
Pour les besoins plus complexes de localisation, les enregistrements de mouvements peuvent être utilisés pour enregistrer avec précision les mouvements d'objets entre les lieux de stockage, lors de prêts ou d'expositions. Utilisés dans le cadre d'une politique de localisation ou d'historique d'utilisation, les mouvements peuvent fournir un enregistrement solide de chaque mouvement dans l'histoire d'un objet.

### Représentations d'objets (ca\_object\_representations)
Les représentations décrivent les médias numériques représentatifs (images, vidéo, audio, PDF) des objets. Les notices de représentation ne contiennent généralement qu'un fichier multimédia, mais peuvent contenir un catalogage supplémentaire spécifique au fichier multimédia (et non à l'objet que le fichier dépeint ou représente) si cela est souhaité. Lorsqu'elles sont utilisées, les métadonnées de représentation comprennent souvent des légendes, des crédits, des informations d'accès, des droits et des restrictions de reproduction.

### Parcours de visite (ca\_tours)
Les enregistrements de parcours saisissent des informations sur les visites sur place ou en ligne d'objets, de lieux, de collections ou de tout autre enregistrement de la base de données.

### POIs du parcours (ca\_tour\_stops)
Chaque parcours de visite comporte un nombre quelconque de points d’intérêt (POIs) ordonnés. Chaque POIs contient des métadonnées sur l’arrêt (texte descriptif, coordonnées géographiques, etc.) ainsi que des relations avec des objets et des entités pertinents, etc.

### Tables de label
Les labels sont des noms ou des titres d'enregistrements. Toutes les tables primaires sont accompagnées de tables de labels. Il existe deux types de labels : les labels préférés et les labels non préférées. Chaque enregistrement possède une, et un seul, label préféré. Le label préféré est utilisée comme titre d'affichage par défaut de l'enregistrement. Les enregistrements peuvent avoir un nombre quelconque de labels non préférés, qui sont considérés comme des titres alternatifs et peuvent être utilisées dans les recherches. Les labels sont toujours présents et n'ont pas besoin d'être configurés pour exister.

L'abréviation suivante est couramment utilisée pour référencer les libellés préférés : <tablename>.preferred\_labels.<label table name field>. Par exemple, le label préféré d'un objet se code comme suit :
```
ca_objects.preferred_labels.name
```

Voir les champs de labels ci-dessous pour les champs de nom spécifiques aux tables.

## Eléments de métadonnées

### Types d’attributs de métadonnées
Les types d'attributs représentent toutes les variétés de champs prises en charge par CollectiveAccess. Chacun d'entre eux est légèrement différent car il est conçu pour accepter et normaliser des données dans des formats différents. Voir ci-dessous pour plus de détails sur la nature unique de chaque type d'attribut. La liste complète des types d'attributs se trouve ici.

**Conteneur (container)**
Contrairement à tous les autres types d'attributs, les conteneurs ne représentent pas de valeurs de données. Leur seule fonction est d'organiser les attributs en groupes pour l'affichage. Dans un ensemble de valeurs multi-attributs (par exemple une adresse avec des attributs distincts pour le numéro de rue, la ville, l'État, le pays et le code postal), il y aura au moins un conteneur servant de "racine" (ou de sommet) de la hiérarchie des attributs. D'autres conteneurs peuvent servir à regrouper les éléments de l'ensemble d'attributs multiples en sous-groupes affichés sur des lignes distinctes d'un formulaire.

**Texte (text)**
Représente une valeur en texte libre.

**Date (DateRange)**
Représente une plage de dates historiques acceptant des expressions de plage de dates et d'heures dans les formats acceptés par le module CA TimeExpressionParser.

**Liste (list)**
Représente une valeur choisie dans une liste déroulante remplie de valeurs provenant d'une liste spécifiée, telle que définie dans la table ca_lists.

**Geocode**
Représente une ou plusieurs coordonnées de latitude/longitude. Les coordonnées peuvent être saisies sous forme de paires décimales latitude/longitude (ex. 40.321,-74.55) ou au format degrés-minutes-secondes (ex. 40° 23' 10N, 74° 30' 5W). Les coordonnées multiples de latitude/longitude doivent être séparées par des points-virgules (" ;"). Les entrées non coordonnées sont converties en coordonnées à l'aide du service de géocodage de Google Maps, qui fonctionne bien pour la plupart des adresses complètes et partielles dans le monde entier. Pour distinguer sans ambiguïté les données de coordonnées des données d'adresses à géocoder, il est fortement conseillé de placer les listes de coordonnées entre crochets 
```
[40.321,-74.55;41.321,-74.55;41.321,-75.55;40.321,-75.55;40.321,-74.55]
```

**URL**
Accepte une valeur URL correctement formatée. Actuellement, la vérification de la syntaxe générale et du protocole spécifié est assez limitée. Il pourrait être étendu à l'avenir pour vérifier le code de retour HTTP de l'URL.

**Devise (Currency)**
Accepte une valeur monétaire composée d'un spécificateur de devise et d'un nombre décimal. Le spécificateur actuel doit être un code de devise standard à trois lettres (voir http://www.xe.com/iso4217.php) ou l'un des symboles de devise spéciaux suivants : $ (dollar américain), ¥ (yen japonais), £ (livre anglaise) ou € (euro). Exemples d'entrées valides : $14.95, £32.50, CAD 20, DKK 75.

**Longueur (length)**
Accepte les mesures de longueur en unités métriques, anglaises et en points (ces derniers étant des points typographiques). Les entrées sont simplement une quantité numérique + un spécificateur d'unité. Les spécificateurs d'unités pris en charge sont décrits sur la page des formats d'entrée des mesures. Alors que toute unité de longueur prise en charge peut être utilisée pour l'entrée, les unités d’affichage ou d’export sont dictées par les préférences de l'utilisateur en matière d'unités. Cette préférence peut être réglée pour utiliser les unités anglaises, les unités métriques ou pour afficher la mesure en utilisant les unités avec lesquelles elle a été initialement saisie.

**Poids (weight)**
Accepte les mesures de poids en unités métriques et anglaises. Les entrées sont simplement une quantité numérique + un spécificateur d'unité. Les spécificateurs d'unités pris en charge sont décrits sur la page des formats d'entrée des mesures. Alors que toute unité de poids prise en charge peut être utilisée pour l'entrée, les unités d’affichage ou d’export sont dictées par un paramètre des préférences de l'utilisateur. Cette préférence peut être réglée pour utiliser les unités anglaises, les unités métriques ou pour afficher la mesure en utilisant les unités avec lesquelles elle a été initialement saisie.

**TimeCode**
Accepte les décalages temporels dans un certain nombre de formats de code temporel. Les valeurs de code temporel sont généralement utilisées pour exprimer une durée ou une position temporelle dans un média basé sur le temps (par exemple, un emplacement dans un flux vidéo ou audio). Les formats pris en charge sont les suivants : hh:mm:ss (ex. 2:10:52 = 2 heures, 10 minutes, 52 secondes) ; XXh XXm XXs (ex. 2h 10m 52s) ; ou XXs (ex. 7852s = 7852 secondes).

**Entier (integer)**
Accepte les valeurs entières, mais pas les valeurs flottantes. En fait, tout ce qui contient uniquement les chiffres 0-9 est accepté.

**Numérique (numeric)**
Accepte les valeurs numériques. Les chaînes numériques se composent d'un signe facultatif, d'un nombre quelconque de chiffres, d'une partie décimale facultative et d'une partie exponentielle facultative. Ainsi, +0123.45e6 est une valeur numérique valide. La notation hexadécimale (0xFF) est également autorisée, mais uniquement sans le signe, la partie décimale et la partie exponentielle.

**LCSH**
Valeur de la vedette-matière de la Library of Congress. Prend la vedette des LCSH ou la première partie de la vedette (le service de recherche des LCSH ne prend en charge que les recherches par troncature), effectue une recherche et renvoie une liste de correspondances possibles. La vedette LCSH sélectionnée est stockée sous forme de texte et d'identifiant URL du service.

**Geonames**
Valeur GeoNames. Prend le texte de la recherche, le transmet au service de recherche GeoNames et fournit une liste déroulante avec les résultats de la recherche (classés par score). Le nom géographique sélectionné est stocké sous forme de texte (nom, pays, continent et ID) et d'identifiant URL du service.

**Fichier (file)**
Fichier téléchargé. L'autorité de certification tentera d'identifier le fichier et d'extraire des métadonnées limitées, mais même si elle ne parvient pas à identifier le fichier, elle l'acceptera et le stockera.

**Media**
Média téléchargé (image, son, vidéo). L'autorité de certification tentera d'identifier le fichier, d'extraire les métadonnées et de créer des produits dérivés conformément à la configuration du fichier media\_processing.conf. Si l'autorité de certification ne peut pas identifier et analyser le fichier, elle le rejettera.

**Taxonomie (taxonomy)**
Nom taxonomique tel qu'il est renvoyé par un service de noms taxonomiques. Prend actuellement en charge les recherches dans les services ITIS et uBio.

**Service d'information (InformationService)**
Consultation à distance de services web. Consultation des valeurs des services web, y compris le Getty TGN, ULAN et AAT, une autre instance de CollectiveAccess, Wikipedia, WorldCat et uBio.

**Représentations d'objets (ObjectRepresentations)**
Références à des représentations d'objets au sein de votre instance CollectiveAccess.

**Entités (entities)**
Valeur de l'entité. Recherche dans l'autorité de l'entité CollectiveAccess le texte donné et crée une pseudo-relation sans type avec l'entité sélectionnée.

**Lieux (places)**
Valeur de lieu. Recherche l'autorité de lieu CollectiveAccess pour un texte donné et crée une pseudo-relation sans type avec le lieu sélectionné. Peut être limité à un seul type de lieu.

**Occurrences**
Valeur d'occurrence. Recherche l'autorité d'occurrence CollectiveAccess pour un texte donné et crée une pseudo-relation sans type avec l'occurrence sélectionnée. Peut (et doit) être limité à un seul type d'occurrence.

**Collections**
Valeur de la collection. Recherche dans l'autorité de collection CollectiveAccess un texte donné et crée une pseudo-relation sans type avec la collection sélectionnée (sans type). Peut être limité à un seul type d'occurrence.

**Emplacements de stockage**
Valeur de l'emplacement de stockage. Recherche dans l'autorité des emplacements de stockage CollectiveAccess un texte donné et crée une pseudo-relation sans type avec l'emplacement de stockage sélectionné (sans type). Peut être limité à un seul type d'emplacement de stockage.

**Prêts (loans)**
Valeur du prêt. Recherche dans l'autorité de prêt CollectiveAccess le texte donné et crée une pseudo-relation sans type avec le prêt sélectionné (sans type). Peut être limité à un seul type d'occurrence.

**Mouvements (movements)**
Valeur du mouvement. Recherche dans l'autorité de mouvement CollectiveAccess le texte donné et crée une pseudo-relation sans type avec le mouvement sélectionné (sans type). Peut être limité à un seul type de mouvement.

**Objets (objects)**
Valeur de l'objet. Recherche dans l'autorité des objets CollectiveAccess un texte donné et crée une pseudo-relation sans type avec l'objet sélectionné (sans type). Peut être limité à un seul type d'objet.

**Lots d’objets (ObjectLots)**
Valeur du lot d'objets. Recherche dans l'autorité des lots d'objets de CollectiveAccess le texte donné et crée une pseudo-relation sans type avec le lot d'objets sélectionné (sans type). Peut être limité à un seul type de lot d'objets.

**Plan d'étage (floorplan)**
Mise en place d'une interface utilisateur interactive pour les plans d'occupation des sols pour les enregistrements d'autorité de lieu

**Couleur (color)**
Représente une couleur au format hexadécimal RVB standard (ex. FFCC33). Dans l'interface d'édition, ce type de données est généralement affiché avec un sélecteur de couleurs.

**Taille de fichier (filetiez)**
Accepte les valeurs de taille des fichiers numériques avec les suffixes couramment utilisés (B, KB, KiB, MB, MiB, GB, GiB, TB, TiB, PB, PiB). Disponible à partir de la version 1.8.

### Paramètres spécifiques en fonction du type de métadonnée

Consulter la page [https://manual.collectiveaccess.org/providence/user/dataModelling/metadata/AttributeTypeSettings.html] (en anglais)
