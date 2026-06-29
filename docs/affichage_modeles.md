# Syntaxe des modèles d'affichage

Les modèles d'affichage servent à mettre en forme les données issues des blocs (les éléments de métadonnées stockés dans CollectiveAccess) pour l'affichage à l'écran, la production d'éditions et la présentation des résultats de recherche. En l'absence de modèle d'affichage défini, CollectiveAccess restitue les données du bloc de la façon la plus simple possible, en général sous forme de liste de valeurs séparées par des points-virgules. Pour les blocs constitués d'une seule valeur (par exemple un simple élément de métadonnée texte), c'est souvent suffisant. Pour les blocs complexes composés de plusieurs valeurs distinctes — une adresse postale par exemple — un modèle est généralement nécessaire pour mettre en forme la valeur correctement. Les modèles d'affichage de blocs sont également utiles dans les cas suivants :

- Pour définir la mise en forme : titres, gras et italiques autour des éléments du bloc.
- Pour mettre en forme et insérer conditionnellement des séparateurs et des suffixes entre les valeurs d'un bloc complexe. Par exemple, dans un bloc avec des dimensions largeur, longueur et hauteur, on peut placer un séparateur « x » entre chaque dimension. Un affichage permet de restituer les valeurs dans l'ordre largeur/longueur/hauteur (ou tout autre ordre). Ainsi un bloc avec longueur = 24", hauteur = 8" et largeur = 3" peut être restitué en 3" x 24" x 8"… ou 3"l x 24"L x 8"H… ou 3"l x 8"H si la longueur n'est pas renseignée (car les affichages savent omettre intelligemment le séparateur et le suffixe).
- Pour afficher des données rattachées à des enregistrements liés. Par exemple, pour afficher à la fois le nom et les dates de vie d'entités liées, un modèle d'affichage de bloc peut extraire et mettre en forme ces données. Toute donnée rattachée à l'entité liée peut être affichée.
- Pour afficher des données liées en traversant un nombre quelconque de relations intermédiaires. Exemple simple : imaginons un objet lié à une collection, elle-même liée à un donateur. Il n'est pas nécessaire de cataloguer le donateur directement sur l'objet pour afficher son adresse ici, puisqu'il est possible de remonter l'adresse à travers la relation avec la collection. Autre exemple courant dans les archives du film et du spectacle : des objets peuvent être liés à des « œuvres » (occurrences) qui ont elles-mêmes des relations avec des entités (« réalisateur », « acteur », « chorégraphe »). Un modèle d'affichage peut présenter les informations de l'objet aux côtés des données d'entité liées à une œuvre, elle-même liée à l'objet.
- Pour appliquer l'un de plusieurs formats d'affichage en fonction de conditions portant sur une ou plusieurs valeurs de données.

Les modèles d'affichage sont également très utilisés par Pawtucket 2.0 pour la mise en forme dans les thèmes. C'est la méthode de mise en forme privilégiée dans Pawtucket 2.0, même si le code mixte HTML/PHP reste pris en charge.

## Définir des modèles

Des modèles d'affichage par défaut peuvent être définis pour les éléments de métadonnées dans le cadre de leur configuration. Cette mise en forme par défaut peut être surchargée par des modèles supplémentaires propres à un contexte, au sein d'un affichage ou d'une interface utilisateur.

Le modèle par défaut d'un élément de métadonnée se définit dans l'interface de configuration. Les modèles liés à un affichage ou à une interface utilisateur se définissent dans leurs éditeurs de configuration respectifs, bloc par bloc. Lorsqu'un modèle est défini pour un élément de métadonnée au sein d'un affichage ou d'une interface utilisateur de saisie, il prend le pas sur les modèles définis dans la configuration de l'élément.

## Syntaxe des modèles

Dans leur forme la plus simple, les modèles ne sont que du texte contenant des marqueurs destinés à être remplacés par les valeurs des blocs. Un marqueur commence toujours par un accent circonflexe (`^`) suivi d'un spécificateur de bloc, un identifiant non ambigu d'élément de métadonnée. Par exemple, si vous avez dans une fiche objet un élément de métadonnée dont le code est `description` et que vous souhaitez préfixer sa valeur par l'intitulé « Description : », le modèle serait :

```text
Description : ^ca_objects.description
```

où `ca_objects` indique une fiche objet et `description` est le code de l'élément de métadonnée.

Si la valeur de l'élément `description` est vide, ce modèle affichera l'intitulé « Description : » sans valeur à la suite, ce qui est disgracieux. Pour éviter les espaces vides indésirables, on peut conditionner un modèle d'affichage à la présence d'une valeur dans un champ. Un modèle qui n'affiche quelque chose que si une description est disponible ressemblerait à ceci :

```text
<ifdef code="ca_objects.description">Description : ^ca_objects.description</ifdef>
```

Tout ce qui se trouve entre `<ifdef>` et `</ifdef>` n'est restitué pour le bloc correspondant (indiqué sans le `^` dans la balise `<ifdef>`, car il s'agit ici d'un code et non d'un marqueur) que lorsque ce bloc a effectivement une valeur.

La sortie conditionnelle ne sert pas qu'aux intitulés. Pour les dimensions et autres ensembles de quantités, elle permet de gérer les cas où toutes les valeurs ne sont pas disponibles. Par exemple, supposons un conteneur de métadonnées nommé `dimensions` sur une fiche objet, avec trois sous-éléments : width, height et depth, tous de type Longueur. Afficher le conteneur `ca_objects.dimensions` sans modèle produirait trois valeurs séparées par des points-virgules, le séparateur par défaut :

```text
12"; 6"; 9"
```

(on suppose ici un affichage en unités anglo-saxonnes)

Pour le rendre plus clair, on peut mettre en forme le conteneur avec ce modèle :

```text
^ca_objects.dimensions.width l x ^ca_objects.dimensions.height H x ^ca_objects.dimensions.depth P
```

Ce qui affichera :

```text
12" l x 6" H x 9" P
```

Comme on le voit, une syntaxe particulière est utilisée pour exprimer les éléments d'un conteneur. Ce n'est plus seulement `^ca_objects.dimensions` dans notre exemple, mais le code du conteneur parent accompagné du sous-élément précis que vous voulez afficher.

Si la valeur depth est vide dans certains cas, la sortie ressemblerait parfois à ceci :

```text
12" l x 6" H x P
```

Pour corriger cela, on utilise la sortie conditionnelle :

```text
<ifdef code="ca_objects.dimensions.width">^ca_objects.dimensions.width l x</ifdef>
<ifdef code="ca_objects.dimensions.height">^ca_objects.dimensions.height H x</ifdef>
<ifdef code="ca_objects.dimensions.depth">^ca_objects.dimensions.depth P</ifdef>
```

On peut aussi utiliser les conditions pour supprimer l'espace entre `^ca_objects.dimensions.width` et le « l », `^ca_objects.dimensions.height` et le « H », `^ca_objects.dimensions.depth` et le « P ». Normalement, un espace est requis entre le marqueur et tout texte qui n'est pas un marqueur, afin de délimiter clairement la fin du marqueur. Avec une condition, vous pouvez séparer le marqueur du texte sans recourir à des espaces, comme dans cet exemple :

```text
^ca_objects.dimensions.width<ifdef code="ca_objects.dimensions.width">l x</ifdef> ^ca_objects.dimensions.height<ifdef code="ca_objects.dimensions.height">H x</ifdef> ^ca_objects.dimensions.depth<ifdef code="ca_objects.dimensions.depth">P</ifdef>
```

Si vous devez conditionner une partie de votre modèle à la présence de plusieurs valeurs, listez simplement les noms de marqueurs dans la valeur de `code`, séparés par des virgules :

```text
<ifdef code="ca_objects.dimensions.width,ca_objects.dimensions.height,ca_objects.dimensions.depth">Dimensions : </ifdef>^ca_objects.dimensions.width<ifdef code="ca_objects.dimensions.width">l x</ifdef> ^ca_objects.dimensions.height<ifdef code="ca_objects.dimensions.height">H x</ifdef> ^ca_objects.dimensions.depth<ifdef code="ca_objects.dimensions.depth">P</ifdef>
```

« Dimensions : » ne sera affiché que si width, height et depth ont tous une valeur. Pour que le texte s'affiche dès qu'au moins une des valeurs de la liste `code` est renseignée, séparez les noms de marqueurs par des barres verticales (`|`, le caractère « pipe ») :

```text
<ifdef code="ca_objects.dimensions.width|ca_objects.dimensions.height|ca_objects.dimensions.depth">Dimensions : </ifdef>^ca_objects.dimensions.width<ifdef code="ca_objects.dimensions.width">l x</ifdef> ^ca_objects.dimensions.height<ifdef code="ca_objects.dimensions.height">H x</ifdef> ^ca_objects.dimensions.depth<ifdef code="ca_objects.dimensions.depth">P</ifdef>
```

Dans certains cas, vous aurez besoin de conditionner une partie de modèle à l'**absence** d'une ou plusieurs valeurs. La balise `<ifnotdef>` le permet, de façon symétrique à `<ifdef>`. Par exemple, pour afficher un message « Aucune dimension » quand aucune valeur n'est définie :

```text
<ifnotdef code="ca_objects.dimensions.width,ca_objects.dimensions.height,ca_objects.dimensions.depth">Aucune dimension renseignée</ifnotdef>^ca_objects.dimensions.width<ifdef code="ca_objects.dimensions.width">l x</ifdef> ^ca_objects.dimensions.height<ifdef code="ca_objects.dimensions.height">H x</ifdef> ^ca_objects.dimensions.depth<ifdef code="ca_objects.dimensions.depth">P</ifdef>
```

## Options de marqueur

La valeur d'un marqueur peut être modifiée par des options ajoutées sous forme de paramètres nommés. Les options sont séparées du marqueur par un caractère `%` et listées en paires `<nom>=<valeur>` délimitées par des caractères `&` ou `%` (le `&` est utilisé dans les anciens modèles, mais peut désormais s'employer indifféremment avec `%`). Par exemple :

```text
^ca_objects.hierarchy.preferred_labels.name%maxLevelsFromBottom=4&delimiter=_➜_
```

affichera une liste de titres d'objets hiérarchiques composée des quatre derniers titres en partant du bas, séparés par des flèches. Sans ces options, les valeurs par défaut s'appliqueraient : ici, la hiérarchie entière séparée par des points-virgules.

On peut ajouter autant d'options que l'on veut à un marqueur.

Notez que les espaces sont interdits dans les options, car ils servent à séparer les marqueurs. Utilisez l'encodage URL (par exemple `%20` pour un espace) ou des tirets bas à la place des espaces.

Les options suivantes permettent de mettre en forme la valeur texte de n'importe quel marqueur :

| Option | Description |
|---|---|
| `toUpper` | Force le texte tout en majuscules lorsqu'elle vaut une valeur non nulle. |
| `toLower` | Force le texte tout en minuscules lorsqu'elle vaut une valeur non nulle. |
| `makeFirstUpper` | Met la première lettre en majuscule lorsqu'elle vaut une valeur non nulle. |
| `useSingular` | Convertit le label au singulier lorsqu'elle vaut une valeur non nulle. |
| `trim` | Supprime les espaces en début et fin de valeur. |
| `start` | Coupe le début du texte pour qu'il commence au caractère indiqué ; ex. « This is a test » avec `start=2` devient « is is a test ». |
| `length` | Tronque le texte au nombre de caractères indiqué. Combinable avec `start` pour extraire des portions de texte, ou seule pour garantir une longueur maximale. |
| `truncate` | Tronque le texte à la longueur maximale indiquée. Équivaut à `start=0` avec `length` réglée sur la longueur de troncature. |
| `ellipsis` | Ajoute des points de suspension (« … ») au texte tronqué lorsqu'elle vaut une valeur non nulle. Le texte obtenu fait la longueur indiquée, points de suspension compris. Ainsi un texte tronqué à 12 caractères comprend 9 caractères de texte et 3 caractères de points de suspension. |

Pour les options booléennes simples vrai/faux comme `toUpper`, vous pouvez omettre le `=` et la valeur. Ces deux modèles sont équivalents :

```text
^ca_objects.preferred_labels.name%trim=1
```

et

```text
^ca_objects.preferred_labels.name%trim
```

## Remonter des métadonnées à travers une relation

Dans les exemples précédents, les données affichées proviennent toujours d'une fiche objet donnée — l'enregistrement « primaire ». Les modèles sont toujours évalués relativement à l'enregistrement primaire. Si vous mettez en forme des résultats de recherche d'objets, par exemple, votre modèle sera évalué de façon répétée pour chaque objet du jeu de résultats, chaque objet devenant tour à tour le primaire. C'est évident mais utile à rappeler : les marqueurs renvoyant directement à des données du primaire (`^ca_objects.idno` par exemple) tirent leur valeur du primaire. Si un bloc se répète pour un enregistrement, vous pouvez obtenir plusieurs valeurs, mais toutes les valeurs renvoyant au primaire seront toujours prises sur le primaire. N'importe quel enregistrement peut être primaire. Le caractère « primaire » est simplement le contexte dans lequel un modèle est évalué.

Il est souvent nécessaire d'afficher des métadonnées issues d'enregistrements liés au primaire. Par exemple, vous pourriez vouloir afficher les entités liées à un objet (le primaire) en présentant la période de vie et le lieu de naissance de chaque entité à côté de son nom. Ou afficher les collections liées, avec le nom, les restrictions d'accès et les informations de disponibilité. Ou encore un affichage des objets liés à l'objet primaire courant.

Pour les cas simples, afficher des données liées ressemble à afficher des données du primaire. Pour les marqueurs qui renvoient à des données non primaires, CollectiveAccess recherche les enregistrements de ce type directement liés au primaire. Pour un marqueur `^ca_entities.preferred_labels.displayname` dans un affichage de résultats d'objets, CollectiveAccess remontera les noms de toutes les entités directement liées à l'objet primaire. Avec nos données d'exemple :

```text
^ca_entities.preferred_labels.displayname
```

produira une liste de noms d'affichage des entités liées, séparés par des points-virgules (le séparateur par défaut) :

```text
George Tilyou; Elmer Dundy
```

Pour remonter des données d'enregistrements liés du même type que le primaire (ex. des objets liés à un objet), ajoutez `related` au spécificateur de bloc :

```text
^ca_objects.related.preferred_labels.displayname
```

Avec nos données d'exemple, cela renverra le titre de l'objet lié au primaire. Vous pouvez inclure `related` dans les spécificateurs pour tout type d'enregistrement lié, mais ce n'est nécessaire que lorsque les choses seraient ambiguës sans lui.

Vous pouvez remonter n'importe quelle donnée des fiches d'entités liées à l'aide de marqueurs construits de la même façon. Par exemple, ce modèle :

```text
^ca_entities.preferred_labels.displayname (Dates de vie : ^ca_entities.life_span)
```

renverra :

```text
George Tilyou; Elmer Dundy; (Dates de vie : 1865 - 1914; 1862 - 1907)
```

Chaque marqueur est évalué séparément et une liste de valeurs est renvoyée à sa place. Pour mettre en forme plusieurs données liées dans un bloc cohérent, afficher des données liées indirectement (comme les lieux de naissance de l'entité liée), définir des séparateurs personnalisés et d'autres options, une nouvelle directive de modèle est nécessaire : la balise `<unit>`.

## Mettre en forme avec `<unit>`

Les balises `<unit>` permettent de découper vos modèles en sous-modèles évalués indépendamment, puis réassemblés pour la sortie finale. Grâce à l'attribut `relativeTo` de `<unit>`, l'enregistrement primaire du modèle peut être transformé en un ou plusieurs enregistrements liés, en valeurs répétées du primaire (par exemple les valeurs d'un conteneur répétable) ou en un ensemble de valeurs hiérarchiques, et le sous-modèle est évalué pour chacun.

`<unit>` et `relativeTo` permettent une foule de transformations de mise en forme utiles (et souvent complexes) :

- Lorsqu'un enregistrement comporte des conteneurs répétables. Imaginons un conteneur d'adresse répétable sur une fiche entité, pour gérer plusieurs changements d'adresse. Si vous mettez en forme votre modèle sans préciser que chaque occurrence du conteneur doit être affichée comme une unité, le résultat sera une seule adresse, quel que soit le nombre d'adresses saisies, et chaque marqueur contiendra les valeurs de toutes les adresses — une façon absurde d'afficher une liste d'adresses. Encadrer la partie adresse du modèle par des balises `<unit>` et préciser qu'elle doit être évaluée relativement à l'élément adresse répétable, plutôt qu'au primaire lui-même, force le modèle contenu à être évalué une fois par valeur d'adresse répétée, produisant une valeur mise en forme indépendamment pour chaque adresse. Ex. :

```
<unit relativeTo="ca_entities.address">
^ca_entities.address.street_address<br/>^ca_entities.address.city, ^ca_entities.address.state ^ca_entities.address.zip_code<br/>
</unit>
```

  L'option `relativeTo` de la balise `<unit>` force le sous-modèle à être évalué une fois par valeur d'adresse de l'enregistrement primaire.

- Lorsque vous devez présenter côte à côte plusieurs données issues d'enregistrements liés. Dans la section précédente, on a vu que différents marqueurs renvoyant aux mêmes enregistrements liés produisent toujours des listes séparées, une par marqueur. Affichées côte à côte, le résultat est une série de listes plutôt que les blocs distincts de sortie pour chaque élément lié, généralement souhaités. Les balises `<unit>` permettent de définir des sous-modèles évalués de façon répétée, autant de fois qu'il y a d'enregistrements liés. Notre exemple de la section précédente, reformulé avec des balises `<unit>` :

```text
<unit relativeTo="ca_entities">^ca_entities.preferred_labels.displayname (Dates de vie : ^ca_entities.life_span)</unit>
```

  donne ce résultat :

```text
George Tilyou (Dates de vie : 1865 - 1914); Elmer Dundy (Dates de vie : 1862 - 1907)
```

  Ici, l'option `relativeTo` de `<unit>` déplace l'enregistrement primaire vers chaque entité liée tour à tour, dans le seul sous-modèle défini par `<unit>`.

- Lorsque vous devez définir des options d'affichage pour une partie de modèle. Les balises `<unit>` offrent des options pour modifier la sortie des sous-modèles. Vous pouvez définir le séparateur des valeurs répétées avec l'option `delimiter`, ou restreindre les éléments liés affichés par type de relation ou par type d'élément lié avec respectivement `restrictToRelationshipTypes` et `restrictToTypes` (ou leurs contreparties `excludeRelationshipTypes` et `excludeTypes`). (Vous pouvez aussi définir des options sur des marqueurs individuels, mais déclarer les options sur les balises `<unit>` est généralement plus pratique et toujours plus lisible.) Ex. :

```
<unit relativeTo="ca_entities" restrictToRelationshipTypes="actor, director, producer">
^ca_entities.preferred_labels.displayname (Dates de vie : ^ca_entities.life_span)
</unit>
```

- Lorsque vous devez afficher des métadonnées relatives à des enregistrements hiérarchiques. Sans la balise `<unit>`, impossible de lister individuellement les enregistrements enfants et leurs métadonnées dans un affichage. Avec `<unit>`, vous pouvez afficher les enregistrements parents et/ou enfants et les chemins hiérarchiques sous forme d'unités distinctes et complexes, en rendant l'unité `relativeTo` l'ensemble hiérarchique. Ex. :

```text
<unit relativeTo="ca_list_items.hierarchy"><p>^ca_list_items.preferred_labels.name_plural (ca_list_items.idno)</p></unit>
```

  Ici, l'option `relativeTo` de `<unit>` déplace l'enregistrement primaire vers chaque élément de liste de la hiérarchie tour à tour, dans le seul sous-modèle défini par `<unit>`.

- Lorsque vous devez remonter des métadonnées à travers une relation indirecte. Sans la balise `<unit>`, seules les métadonnées d'enregistrements directement liés au primaire peuvent être affichées. Dans nos données d'exemple, cela signifie que seules les entités liées à l'objet primaire peuvent être affichées, mais pas le lieu de naissance lié à chaque entité. En imbriquant des balises `<unit>` les unes dans les autres et en précisant l'option `relativeTo`, on peut déplacer l'enregistrement primaire d'un sous-modèle à travers un nombre quelconque de relations. On pourrait appeler cela « les six degrés de séparation de Kevin Bacon pour CollectiveAccess » où A est lié à B, lui-même lié à C. Par exemple, si le primaire est un objet et que vous devez afficher des données de lieu issues des entités liées aux objets (et non des lieux liés directement à l'objet), le modèle suivant ferait l'affaire :

```
Objet : ^ca_objects.preferred_labels.name;
Entités : <unit relativeTo="ca_entities">^ca_entities.preferred_labels.displayname
(Lieu de naissance : <unit relativeTo="ca_places">^ca_places.preferred_labels.name</unit></unit>
```

  Chaque `unit` déplace le primaire d'un « saut » relationnel. L'imbrication des `<unit>` permet aux déplacements de se cumuler, car ils sont toujours évalués relativement à leur contexte. Ainsi, les entités liées aux objets sont récupérées, puis les lieux liés à ces entités.

### Attributs

Les balises `<unit>` acceptent les attributs suivants :

| Attribut | Description | Par défaut |
|---|---|---|
| `relativeTo` | Transforme l'enregistrement primaire du modèle ou de la `<unit>` englobante (quand les `<unit>` sont imbriquées) en un ensemble d'enregistrements liés, d'enregistrements liés hiérarchiquement ou de valeurs répétées. | Aucun ; doit être défini |
| `restrictToTypes` | Pour les `<unit>` `relativeTo` une relation (ex. `relativeTo='ca_entities'`) ou une hiérarchie (ex. `relativeTo='ca_objects.hierarchy'`, `.parent`, `.siblings`, `.children`), restreint l'ensemble aux enregistrements des types indiqués. Utilisez les identifiants de type, séparés par des virgules. | Aucune restriction |
| `restrictToRelationshipTypes` | Pour les `<unit>` `relativeTo` une relation, restreint l'ensemble aux enregistrements liés par les types de relation indiqués. Utilisez les codes de type de relation, séparés par des virgules. | Aucune restriction |
| `excludeTypes` | Comme `restrictToTypes`, mais exclut les enregistrements des types indiqués. | Aucune restriction |
| `excludeRelationshipTypes` | Comme `restrictToRelationshipTypes`, mais exclut les enregistrements liés par les types de relation listés. | Aucune restriction |
| `sort` | Un ou plusieurs spécificateurs de bloc sur lesquels trier l'ensemble. Les spécificateurs doivent être pertinents pour le type d'enregistrements récupérés par `relativeTo`. | Aucun |
| `sortDirection` | Sens du tri : `ASC` (croissant) ou `DESC` (décroissant). | `ASC` |
| `skipIfExpression` | Une expression à évaluer. Si elle est vraie, la `<unit>` est ignorée et ne produit aucune sortie. Il faut échapper (préfixer d'un `\`) les guillemets entourants lors de l'usage d'expressions. | Aucun |
| `skipWhen` | Teste chaque itération du modèle contre une expression et ignore l'itération si l'expression est vraie. Si défini, toutes les itérations sont générées et testées, même quand `start` et `length` sont définis. | Aucun |
| `start` | Pour les valeurs répétées, l'index de la première valeur à renvoyer. Les index commencent à zéro. Ex. pour commencer à la deuxième valeur, réglez `start` sur 1. | `0` |
| `length` | Le nombre maximal de valeurs à renvoyer. Si non défini, toutes les valeurs sont renvoyées. | aucun |
| `unique` | Supprime les valeurs en double dans l'unité par comparaison directe de chaînes. Si non défini, toutes les valeurs sont renvoyées. | `0` |
| `aggregateUnique` | Supprime les doublons dans les unités en comparant les valeurs individuelles avant leur conversion en chaîne. La différence avec `unique` est subtile : `unique` n'élimine que les listes identiques caractère pour caractère, alors que `aggregateUnique` compare les valeurs sous-jacentes avant mise en chaîne (dédoublonnage plus agressif, insensible à l'ordre). | `0` |
| `omitBlanks` | Supprime les valeurs vides de l'ensemble renvoyé. Par défaut, les valeurs vides sont incluses. (Version 1.7.9) | `0` |
| `filter` | Une expression régulière ou une série de valeurs texte pour filtrer la sortie de l'unité. Les valeurs ne contenant pas le texte indiqué, ou ne correspondant pas à l'expression régulière, sont supprimées. (Version 1.7.9) | |
| `filterNonPrimaryRepresentations` | Pour les unités relatives à `ca_object_representations`, contrôle l'affichage des représentations non primaires. Par défaut `yes` : elles ne sont pas affichées. Réglez sur `0` ou `no` pour les afficher. | `1` |

Vous pouvez limiter le nombre de valeurs renvoyées par une `<unit>` portant sur une valeur répétée à l'aide des attributs `start` et `length` décrits ci-dessus. Vous pouvez afficher un texte indiquant combien de valeurs n'ont pas été montrées à l'aide de la balise `<whenunitomits>` placée après une `<unit>`. Par exemple, pour afficher les 5 premières entités liées puis un message avec le total :

```
<unit relativeTo="ca_entities" delimiter=", " start="0" length="5">^ca_entities.preferred_labels.displayname</unit><whenunitomits> et ^omitcount de plus</whenunitomits>
```

Le marqueur `^omitcount` peut être utilisé à l'intérieur de la balise `<unit>` ou `<whenunitomits>`. La balise `<whenunitomits>` se réfère toujours au nombre de valeurs omises dans la `<unit>` qui la précède dans le modèle, et est supprimée quand aucune valeur de la `<unit>` précédente n'est masquée.

!!! note
    La balise `<unit>` offre de nombreuses possibilités de mise en forme complexe, détaillées avec des exemples dans le chapitre [Les unités `<unit>`](affichage_unites.md).

## Balises contextuelles : `<more>` et `<between>`

Les modèles utilisant `<ifdef>` et `<ifnotdef>` peuvent devenir longs et difficiles à gérer lorsqu'ils comportent de nombreux éléments dépendant de l'état de plusieurs marqueurs. Pour rendre ces modèles plus maniables, deux balises contrôlent la sortie en fonction de leur seule position dans le modèle, évitant les longues listes de noms de marqueurs.

La balise `<more>` affiche son contenu si l'un des marqueurs qui la suivent a une valeur. Ainsi ce modèle :

```text
^ca_objects.description <more><br/>Source : </more>^ca_objects.description_source
```

affichera ceci (en supposant `description` = « Un plat en métal » et `description_source` = « catalogue de vente 1978 ») :

```
Un plat en métal
Source : catalogue de vente 1978
```

Si `description_source` était vide, la sortie serait :

```text
Un plat en métal
```

La balise `<between>` affiche son contenu si des marqueurs situés avant elle dans le modèle, ainsi que le marqueur la suivant immédiatement, ont des valeurs. Cela rend la délimitation de listes de valeurs plus compacte qu'avec `<ifdef>` :

```text
^ca_objects.dimensions.width <between>x</between> ^ca_objects.dimensions.height <between>x</between> ^depth
```

La sortie serait les dimensions renseignées avec un unique séparateur « x » entre chaque paire.

## Balises conditionnelles : `<ifdef>`, `<ifnotdef>`, `<ifcount>`, `<if>`

Comme indiqué plus haut, vous pouvez conditionner l'affichage de portions de modèle en les entourant de balises `<ifdef>` et `<ifnotdef>`. Les deux balises prennent un attribut `code` contenant un ou plusieurs spécificateurs de bloc. Si la valeur du bloc n'est pas vide, `<ifdef>` affiche la portion qu'elle encadre. À l'inverse, si la valeur est vide, `<ifnotdef>` affiche son contenu.

Par exemple :

```text
Titre : ^ca_objects.preferred_labels.name <ifdef code="ca_objects.description">Description : ^ca_objects.description</ifdef>
```

Notez que le spécificateur dans l'attribut `code` n'est pas un marqueur et ne prend donc pas de préfixe `^`.

Vous pouvez conditionner `ifdef` et `ifnotdef` à plusieurs blocs en les listant dans l'attribut `code`, séparés par des virgules ou des barres verticales (`|`). Séparés par des virgules, tous les blocs doivent être définis (`<ifdef>`) ou non définis (`<ifnotdef>`) pour que la balise affiche son contenu. Séparés par des barres verticales, il suffit qu'un seul des blocs soit défini (`<ifdef>`) ou non défini (`<ifnotdef>`).

La balise `<ifcount>` contrôle l'affichage du contenu en fonction du nombre de valeurs disponibles pour le spécificateur de bloc indiqué dans `code`. Elle est utile lorsque vous ne voulez afficher du contenu que si le nombre de valeurs d'un bloc est dans une plage donnée. Par exemple, pour n'afficher une liste d'entités liées que s'il y a entre 2 et 5 relations :

```text
<ifcount code="ca_entities.related" min="2" max="5">Entités liées : ^ca_entities.preferred_labels.displayname</ifcount>
```

Vous pouvez afficher du contenu dès que le nombre dépasse un seuil en omettant l'attribut `max` :

```text
<ifcount code="ca_entities.related" min="2">Entités liées : ^ca_entities.preferred_labels.displayname</ifcount>
```

Si l'attribut `min` est omis, il est supposé valoir zéro.

Pour n'afficher du contenu que lorsque le nombre vaut exactement une valeur, réglez `min` et `max` sur le même nombre :

```text
<ifcount code="ca_entities.related" min="1" max="1">Entité liée : ^ca_entities.preferred_labels.displayname</ifcount>
```

La balise `<if>` offre un contrôle maximal en utilisant des [expressions](affichage_expressions.md) pour déterminer quand le contenu est affiché. Par exemple, pour n'afficher le contenu que si `current` est sélectionné dans la liste déroulante de type d'un conteneur de mention de crédit répétable :

```
<unit relativeTo="ca_objects.credit_line"><if rule="^credit_type =~ /current/">^ca_objects.credit_line.credit_text
(^ca_objects.credit_line.credit_type)</if></unit>
```

L'attribut `rule` doit être une expression valide, qui peut utiliser n'importe quel marqueur valide disponible dans le modèle.

`<ifcount>` et `<ifdef>` incluent les valeurs vides dans leur évaluation. À partir de la version 1.7.9, les valeurs vides peuvent être supprimées en réglant l'option facultative `omitBlanks` sur une valeur non nulle. C'est souvent utile pour la mise en forme. Si `omitBlanks` est défini, `<ifcount>` renvoie le nombre de valeurs non vides et `<ifdef>` n'est vrai que si le bloc a au moins une valeur non vide. Notez que `<if>` ne prend pas en charge l'option `omitBlanks` : vous devez filtrer les valeurs vides dans l'expression.

## Encore plus conditionnel : la balise `<case>`

Il faut parfois choisir l'un de plusieurs modèles selon des critères variables. Par exemple, en listant les entités liées à un objet, vous pourriez vouloir faire varier le texte précédant la liste selon le nombre d'entités. Il existe plusieurs façons de le faire avec les modèles d'affichage, mais la plus propre est la balise `<case>` :

```
<case>
     <ifcount code="ca_entities.related" max="0">Aucune entité liée</ifcount>
     <ifcount code="ca_entities.related" min="1" max="1">Entité liée : ^ca_entities.preferred_labels.name</ifcount>
     <ifcount code="ca_entities.related" min="2">Entités liées : ^ca_entities.preferred_labels.name%delimiter=,_</ifcount>
</case>
```

La balise `<case>` évalue chaque balise `<ifcount>` dans l'ordre et s'arrête à la première qui produit une sortie. Vous pouvez inclure des modèles commençant par `<ifdef>`, `<ifnotdef>` et `<if>` aussi bien que `<ifcount>`. Si une balise `<unit>` est incluse comme dernier modèle d'un `<case>`, elle sert de cas par défaut si aucun autre modèle ne produit de sortie.

Comme les balises `<case>` cessent d'évaluer dès qu'elles trouvent un modèle produisant une sortie, elles constituent généralement la façon la plus performante de choisir un modèle dans une liste de possibilités.

## Expressions

Il est également possible de produire le résultat d'une [expression](affichage_expressions.md) tel quel. Un cas d'usage : rendre certaines statistiques sur vos métadonnées interrogeables. Par exemple, vous pourriez utiliser le pré-remplissage (*Prepopulate*) pour conserver en permanence le nombre actuel de relations d'entité de vos objets dans un champ masqué (mais interrogeable et triable).

L'usage de la balise `<expression>` est simple : tout ce qui se trouve à l'intérieur est traité comme une expression. Vous pouvez utiliser vos marqueurs habituels préfixés par `^` et même des balises `<unit>`. Les balises `<unit>` sont évaluées et remplacées en premier lorsque CollectiveAccess exécute les modèles d'affichage, vous pouvez donc utiliser le résultat d'une `<unit>` dans votre expression. Quelques exemples de base :

```text
<expression>5 + 4</expression>
<expression>length(^ca_objects.preferred_labels)</expression>
```

Celui-ci affiche les noms des entités liées et la longueur de chaque chaîne :

```text
<unit relativeTo="ca_entities">^ca_entities.preferred_labels, <expression>length(^ca_entities.preferred_labels)</expression></unit>
```

Le suivant compte le nombre de relations d'entité de l'enregistrement courant. On utilise une balise `<unit>` pour générer les paramètres de la fonction `sizeof` :

```text
<expression>sizeof(<unit relativeTo="ca_entities" delimiter=",">^ca_entities.entity_id</unit>)</expression>
```

Celui-ci calcule l'âge d'Alan Turing :

```text
<expression>age("23 June 1912", "7 June 1954")</expression>
```

## Mettre en forme les affichages hiérarchiques

De nombreux types d'enregistrements peuvent être organisés hiérarchiquement. Pour récupérer tout ou partie de la hiérarchie en vue d'un affichage, utilisez un spécificateur de bloc hiérarchique. C'est un spécificateur normal auquel on ajoute un modificateur hiérarchique (`hierarchy`, `parent`, `children`).

Par exemple, pour un primaire `object`, un marqueur `^ca_objects.hierarchy.preferred_labels.name` renverra les noms de tous les objets de la hiérarchie, du haut vers le bas. Vous voudrez probablement définir un séparateur entre chaque élément de la hiérarchie. Vous pouvez le faire en ajoutant une option de marqueur : ajoutez un signe pourcentage et `delimiter=<mon séparateur>` au spécificateur de bloc, ainsi :

```text
^ca_objects.hierarchy.preferred_labels.name%delimiter=_➔_
```

Lors de la définition du séparateur, on utilise des **tirets bas** à la place des espaces. Les espaces servent à délimiter les spécificateurs de bloc, le séparateur ne peut donc pas comporter d'espace flottant au-delà de l'espace associé au spécificateur. Les tirets bas seront convertis en espaces à l'affichage.

Vous obtenez plus de contrôle sur les affichages hiérarchiques avec une `<unit>` définie relativement à une hiérarchie. Pour notre primaire objet :

```text
<unit relativeTo="ca_objects.hierarchy">^ca_objects.preferred_labels.name (^ca_objects.idno)</unit>
```

évaluera la `<unit>` pour chaque enregistrement de la hiérarchie tour à tour défini comme primaire. Les données liées sont également accessibles, et des `<unit>` supplémentaires peuvent être imbriquées.

Les modificateurs `parent` et `children` fonctionnent comme `hierarchy`, mais renvoient respectivement le parent immédiat d'un enregistrement ou ses enfants immédiats.

Plusieurs options de marqueur permettent de modifier l'affichage des données hiérarchiques :

| Option | Description | Par défaut |
|---|---|---|
| `delimiter` | Texte à utiliser comme séparateur entre plusieurs valeurs. | `;` |
| `maxLevelsFromTop` | Limite le nombre de niveaux renvoyés à ceux du haut, en commençant par la racine. | Aucun |
| `maxLevelsFromBottom` | Limite le nombre de niveaux renvoyés à ceux du bas, en commençant par le niveau le plus profond. | Aucun |
| `hierarchyDirection` | Ordre de restitution des niveaux hiérarchiques : `asc` (de la racine vers le bas) ou `desc` (de l'enfant le plus éloigné vers la racine). | `asc` |
| `allDescendants` | Renvoie tous les éléments de toute la profondeur de la hiérarchie lors de la récupération des enfants avec le modificateur `children`. Par défaut, seuls les enfants immédiats sont renvoyés. | `FALSE` |

## Créer des liens vers d'autres enregistrements

La balise `<l>` permet de créer des liens dans le modèle. Les liens pointent toujours vers l'enregistrement primaire. Dans Providence, le lien mène à l'**interface d'édition** de l'enregistrement ; dans Pawtucket, il mène à l'**affichage de détail**. Il est possible d'écrire des plugins qui surchargent ce comportement pour créer d'autres types de liens.

N'importe quelle portion du modèle peut devenir un lien. Par exemple, en supposant que le primaire est une entité :

```
<l>^ca_entities.preferred_labels.displayname</l> <ifdef code="ca_entities.address.address1">(</ifdef>^ca_entities.address.address1<ifdef code="ca_entities.address.address1">)</ifdef>
```

Cliquer sur le nom de l'entité dans Providence amènerait le catalogueur vers l'**éditeur** de la fiche entité ; dans Pawtucket, vers le **détail** de l'entité.

Les liens pointent toujours vers l'enregistrement primaire. Si vous utilisez des balises `<l>` à l'intérieur d'une `<unit>`, les liens pointeront vers le primaire de la `<unit>`.

## Utiliser du HTML

Vous pouvez librement utiliser des balises HTML pour la mise en forme dans vos modèles, à condition de respecter les règles et d'écrire un balisage bien formé. Veillez à fermer toute balise ouverte. Les balises spéciales de modèle comme `<ifdef>` comptent dans la bonne formation du balisage, même si elles ne s'affichent pas. Ainsi, ceci est incorrect et s'affichera de façon imprévisible :

```
<l>^ca_occurrences.preferred_labels.names</l> <ifdef code="ca_occurrences.exhibit_date"><b>(Dates : </ifdef>^ca_occurrences.exhibit_date<ifdef code="ca_occurrences.exhibit_date">)</b></ifdef> ^ca_occurrences.description
```

Remarquez que la balise `<b>` du premier `<ifdef>` n'est pas fermée avant le `</ifdef>` fermant, produisant un balisage invalide. Il y a bien une balise `</b>` plus loin, mais elle est elle aussi isolée par les balises `<ifdef>` qui l'entourent. La façon correcte d'écrire ce modèle est :

```
<l>^ca_occurrences.preferred_labels.names</l> <ifdef code="ca_occurrences.exhibit_date"><b>(Dates : ^ca_occurrences.exhibit_date</b></ifdef> ^ca_occurrences.description
```

## Marqueurs spéciaux

Quelques marqueurs ont une signification particulière pour certains types d'enregistrements primaires :

| Marqueur | Description |
|---|---|
| `^date` | Affiche la date courante. Valide dans tout modèle, quel que soit le type de primaire. La date est formatée en « jour mois année » (ex. « 10 janvier 2014 ») sauf si un format est précisé via l'option de marqueur `format`, qui prend une chaîne de formatage de style `date()` de PHP (ex. `^date%format=c`). |
| `^relationship_typename` | Affiche le nom du type de relation lorsque le primaire est un enregistrement de relation tel que `ca_objects_x_entities`. Les modèles remontant des enregistrements liés dans les affichages de blocs sont évalués relativement au primaire représentant la relation, et non l'enregistrement lié. Ce marqueur et les autres `^relationship_*` sont donc disponibles par défaut lors de la remontée de données liées dans les affichages de blocs. |
| `^relationship_type_id` | Le `type_id` numérique interne du type de relation lorsque le primaire est un enregistrement de relation. |
| `^relationship_typecode` | Le code alphanumérique du type de relation lorsque le primaire est un enregistrement de relation. |
| `^primary` | Affiche le nom du primaire du modèle ou du sous-modèle `<unit>` courant. Utile pour le débogage. |
| `^count` | Affiche le nombre de valeurs dans le primaire courant du modèle ou du sous-modèle `<unit>`. |
| `^index` | Affiche l'index (à base 1) de la valeur courante dans le primaire ou le sous-modèle `<unit>`. À mesure qu'une `<unit>` parcourt chaque valeur, `^index` s'incrémente de un jusqu'à atteindre `^count`. |

À partir de la version 1.7.9, plusieurs marqueurs spéciaux sont aussi disponibles pour les représentations d'objet et renvoient des métadonnées propres au média, déjà formatées. Utilisez-les sous la forme `^ca_object_representations.<marqueur>`. Ils servent généralement à formater le texte d'affichage dans les listes de représentations :

| Marqueur | Description | Exemple |
|---|---|---|
| `transcription_count` | Nombre de transcriptions générées par les utilisateurs rattachées à la représentation. | 1 |
| `page_count` | Nombre de pages d'un document multipage. Nul si non applicable. | 10 |
| `preview_count` | Nombre d'aperçus disponibles pour un document multipage ou un média temporel. Nul si non applicable. Synonyme de `page_count`. | 10 |
| `media_dimensions` | Dimensions en pixels du média, formatées pour l'affichage. Option : `version=<version>` (défaut `original`). | 1024p x 2048p |
| `media_duration` | Durée d'un média temporel, formatée. Options : `durationFormat` (`delimited`, `hms`, `hm`, `seconds` ; défaut `hms`) et `version` (défaut `original`). | 1h 24m 10s |
| `media_class` | Type général du média d'origine : `image`, `video`, `audio` ou `document`. | `image` |
| `media_format` | Format du média d'origine, pour l'affichage. | `JPEG, TIFF` |
| `media_filesize` | Taille du fichier média, formatée. Option : `version` (défaut `original`). | `43.2mb` |
| `media_colorspace` | Espace colorimétrique du média, formaté. Option : `version` (défaut `original`). | `RGB, CMYK` |
| `media_resolution` | Résolution en pixels du média, formatée. Peut ne pas être disponible pour tous les formats. Option : `version` (défaut `original`). | `300ppi` |
| `media_bitdepth` | Profondeur de bits du média, formatée. Peut ne pas être disponible pour tous les formats. Option : `version` (défaut `original`). | 8bpp |
| `media_center_x` | Coordonnée X du point de recadrage central défini par l'utilisateur pour une image. Fraction décimale de la largeur de l'image. | 0.43 |
| `media_center_y` | Coordonnée Y du point de recadrage central défini par l'utilisateur pour une image. Fraction décimale de la largeur de l'image. | 0.22 |

## Découper une plage de dates en points de données distincts

Les valeurs de date uniques exprimées sous forme de plages (par exemple 2000-2018) peuvent être décomposées en points de données distincts pour la date de début et la date de fin. Par exemple, si vous souhaitez exporter vers MS Excel avec des colonnes distinctes pour la première et la dernière date de la plage. La syntaxe est la suivante :

```
^ca_objects.your_date_element_code%start_as_iso8601=1
^ca_objects.your_date_element_code%end_as_iso8601=1
```
