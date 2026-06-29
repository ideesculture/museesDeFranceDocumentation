# Métadonnées

Les éléments de métadonnées sont les champs de données configurables qui constituent l'essentiel du schéma propre à votre installation. Chaque élément a un **type d'attribut** qui détermine la nature des données qu'il accepte et la façon dont elles sont normalisées. Chaque type est légèrement différent, conçu pour accepter et normaliser des données dans un format particulier.

!!! note
    La liste complète et à jour des types d'attributs figure dans le fichier [`attribute_types.conf`](https://github.com/collectiveaccess/providence/blob/master/app/conf/attribute_types.conf) du dépôt CollectiveAccess.

## Types d'attributs

| Type | Description |
|---|---|
| `Container` | Contrairement à tous les autres types, les conteneurs ne représentent pas une valeur de donnée. Leur seule fonction est d'organiser des attributs en groupes pour l'affichage. Dans un ensemble à plusieurs attributs (par exemple une adresse avec des attributs distincts pour le numéro, la ville, l'état, le pays et le code postal), il y a au moins un conteneur servant de « racine » (sommet) de la hiérarchie d'attributs. D'autres conteneurs peuvent regrouper les items en sous-groupes affichés sur des lignes distinctes d'un formulaire. |
| `Text` | Représente une valeur en texte libre. |
| `DateRange` | Représente une plage de dates historique, acceptant les expressions de plage de dates/heures dans les formats reconnus par le module TimeExpressionParser de CollectiveAccess. |
| `List` | Représente une valeur choisie dans une liste déroulante alimentée par une liste définie dans la table `ca_lists`. |
| `Geocode` | Représente une ou plusieurs coordonnées latitude/longitude. Saisie en paires décimales (ex. `40.321,-74.55`) ou en degrés-minutes-secondes. Plusieurs coordonnées sont séparées par des points-virgules. Les saisies non coordonnées sont converties via le service de géocodage Google Maps. Pour lever toute ambiguïté, il est fortement conseillé d'entourer les listes de coordonnées de crochets. |
| `Url` | Accepte une URL correctement formatée. Vérification actuellement limitée à la syntaxe globale et au protocole. |
| `Currency` | Accepte une valeur monétaire : un code de devise + un nombre décimal. Code de devise standard à trois lettres (voir ISO 4217) ou symbole spécial (`$`, `¥`, `£`, `€`). Exemples valides : `$14.95`, `£32.50`, `CAD 20`, `DKK 75`. |
| `Length` | Accepte des mesures de longueur en unités métriques, anglo-saxonnes et en points (typographiques). Saisie : quantité numérique + spécificateur d'unité. L'unité de sortie est dictée par la préférence d'unité de l'utilisateur. |
| `Weight` | Accepte des mesures de poids en unités métriques et anglo-saxonnes. Saisie : quantité + unité. L'unité de sortie est dictée par la préférence de l'utilisateur. |
| `TimeCode` | Accepte des décalages temporels en plusieurs formats de time code. Sert généralement à exprimer une durée ou une position dans un média temporel. Formats : `hh:mm:ss` (ex. `2:10:52`), `XXh XXm XXs` (ex. `2h 10m 52s`) ou `XXs` (ex. `7852s`). |
| `Integer` | Accepte les valeurs entières, mais pas les décimaux. En pratique, tout ce qui ne contient que les chiffres 0-9 est accepté. |
| `Numeric` | Accepte les valeurs numériques : signe optionnel, chiffres, partie décimale optionnelle et partie exponentielle optionnelle. Ainsi `+0123.45e6` est valide. La notation hexadécimale (`0xFF`) est aussi autorisée, mais sans signe, décimale ni exposant. |
| `LCSH` | Valeur de vedette-matière de la Bibliothèque du Congrès. Recherche une vedette LCSH et renvoie une liste de correspondances possibles. La vedette sélectionnée est stockée à la fois en texte et comme identifiant URL du service. |
| `GeoNames` | Valeur GeoNames. Transmet le texte de recherche au service GeoNames et propose une liste déroulante de résultats. Le géonom sélectionné est stocké en texte (nom, pays, continent et ID) et comme identifiant URL. |
| `File` | Fichier téléversé. CollectiveAccess tente d'identifier le fichier et d'en extraire des métadonnées limitées, mais l'accepte et le stocke même sans l'identifier. |
| `Media` | Média téléversé (image, son, vidéo). CollectiveAccess tente d'identifier le fichier, d'en extraire les métadonnées et de créer les dérivés configurés dans `media_processing.conf`. S'il ne peut pas identifier et analyser le fichier, il le rejette. |
| `Taxonomy` | Nom taxonomique renvoyé par un service de noms taxonomiques. Prend actuellement en charge les services ITIS et uBio. |
| `InformationService` | Interrogation d'un service web distant : Getty TGN, ULAN et AAT, une autre instance CollectiveAccess, Wikipedia, WorldCat, uBio, etc. |
| `ObjectRepresentations` | Référence des représentations d'objet au sein de votre instance CollectiveAccess. |
| `Entities` | Valeur d'entité. Recherche dans l'autorité des entités et crée une pseudo-relation sans type avec l'entité sélectionnée. |
| `Places` | Valeur de lieu. Recherche dans l'autorité des lieux et crée une pseudo-relation sans type. Restreignable à un seul type de lieu. |
| `Occurrences` | Valeur d'occurrence. Recherche dans l'autorité des occurrences et crée une pseudo-relation sans type. Restreignable (et devrait l'être) à un seul type d'occurrence. |
| `Collections` | Valeur de collection. Recherche dans l'autorité des collections et crée une pseudo-relation sans type. Restreignable à un seul type. |
| `StorageLocations` | Valeur d'emplacement de stockage. Recherche dans l'autorité des emplacements et crée une pseudo-relation sans type. Restreignable à un seul type. |
| `Loans` | Valeur de prêt. Recherche dans l'autorité des prêts et crée une pseudo-relation sans type. Restreignable à un seul type. |
| `Movements` | Valeur de mouvement. Recherche dans l'autorité des mouvements et crée une pseudo-relation sans type. Restreignable à un seul type. |
| `Objects` | Valeur d'objet. Recherche dans l'autorité des objets et crée une pseudo-relation sans type. Restreignable à un seul type. |
| `ObjectLots` | Valeur de lot d'objets. Recherche dans l'autorité des lots et crée une pseudo-relation sans type. Restreignable à un seul type. |
| `Floorplan` | Implémente une interface de plan interactif pour les fiches d'autorité de lieu. |
| `Color` | Représente une couleur au format hexadécimal RVB standard (ex. `FFCC33`). Généralement affiché avec un sélecteur de couleur. |
| `Filesize` | Accepte des tailles de fichier avec suffixes courants (`B`, `KB`, `KiB`, `MB`, `MiB`, `GB`, `GiB`, `TB`, etc.). Depuis la version 1.8. |

!!! info "Source"
    Traduction de la documentation officielle [CollectiveAccess / Providence](https://providence.readthedocs.io/en/latest/), section *Data Modelling — Metadata Elements*. Terminologie alignée sur le fichier de localisation `fr_FR` de l'application.
