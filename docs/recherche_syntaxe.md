# Syntaxe de recherche

Quel que soit le moteur de recherche configuré avec CollectiveAccess, c'est toujours la **syntaxe de recherche Lucene** qui sert à formuler les requêtes. Cela offre une expérience cohérente d'une implémentation à l'autre et tire parti d'une syntaxe bien conçue et largement adoptée. Notez que tous les moteurs ne prennent pas en charge tous les aspects de la syntaxe Lucene. En général, vous pouvez compter sur le fait que les fonctions essentielles sont toujours disponibles : recherches texte, limitation au niveau d'un champ, regroupement entre parenthèses et opérateurs booléens. Des fonctions comme le *boosting*, la correspondance floue et les recherches par plage peuvent ne pas être disponibles dans tous les moteurs.

## Recherches en texte intégral

Pour rechercher dans tous les champs indexés de la base (tels que définis dans le fichier de configuration `search_indexing.conf`), tapez simplement un ou plusieurs mots. Selon le moteur, votre saisie peut être racinisée (les suffixes sont retirés avant comparaison avec l'index) pour améliorer les résultats. La plupart des moteurs ne renvoient que les résultats contenant tous les mots indiqués, mais certains peuvent appliquer une logique renvoyant des correspondances partielles jugées pertinentes.

## Limiter votre recherche à un champ précis

Pour restreindre votre recherche à un champ précis de la base CollectiveAccess, indiquez le nom de la table et le champ séparés par un point :

```
<table>.<champ>   (ex. ca_object_labels.name)
```

Une requête de la forme

```
ca_object_labels.name:Rollercoasters
```

ne renverrait que les objets dont le label (par exemple le titre) contient le mot « rollercoasters ».

Notez que cela ne s'applique qu'aux champs « intrinsèques » codés en dur dans la base CollectiveAccess. Ils sont toujours présents quelle que soit votre configuration — même si vous ne les utilisez pas. Seuls quelques champs de ce type sont d'usage courant : les champs de label (pour `ca_objects`, `ca_entities`, etc.), les champs d'identifiant `idno` (pour `ca_objects`, `ca_entities`, etc.), et les champs `extent` et `extent_units` (pour `ca_objects` et `ca_object_lots`).

## Limiter votre recherche à un élément de métadonnée précis

Les éléments de métadonnées sont des champs de données propres à votre installation. Ils peuvent exister ou non dans d'autres installations. La recherche sur ces champs est semblable à celle sur les champs intrinsèques :

```
<ca_table>.<code de l'élément>   (ex. ca_objects.description pour chercher dans l'élément « description » rattaché aux objets)
```

Vous pouvez voir la liste de tous les éléments de métadonnées (et leurs codes) disponibles dans votre configuration via l'éditeur d'éléments de métadonnées, accessible sous l'option « Configuration du système » du menu « Gérer ». (Note : seuls les administrateurs système ont accès à cet éditeur.)

Dans tous les moteurs, vous pouvez effectuer des recherches texte sur n'importe quel élément. Dans certains moteurs — en particulier le moteur MysqlFulltext, moteur par défaut à l'installation — vous pouvez aussi effectuer des recherches spécialisées sur certains types d'éléments, décrites dans les sections suivantes.

## Limiter les recherches à des types de relation précis

Par défaut, lors d'une recherche sur du contenu lié (par exemple rechercher des objets via les noms des entités liées), toutes les relations sont prises en compte. Pour limiter votre recherche à des types de relation précis, ajoutez le code du type de relation (ou les codes, séparés par des virgules) après le qualificateur de champ et une barre oblique. Par exemple, cette requête :

```
ca_entities.preferred_labels.displayname/depicts:"Cynthia Hopkins"
```

utilisée pour trouver des objets renverra tous les objets liés à Cynthia Hopkins par une relation « depicts » (représente).

!!! tip "Complément idéesculture"
    La barre verticale `|` est acceptée à la place de la barre oblique : `ca_entities.preferred_labels.displayname|depicts:"Cynthia Hopkins"`. C'est utile quand la requête est transmise dans une URL, où la barre oblique pose des problèmes d'encodage.

## Rechercher sur des dates

Pour rechercher sur une date ou une plage de dates, restreignez votre recherche à un élément de type plage de dates puis recherchez la date voulue, dans l'un des formats décrits sur la page des formats de date et d'heure. Vous pouvez utiliser tout format pris en charge et toute précision : le moteur trouvera toute date (et éventuellement heure) qui chevauche votre plage de recherche. La correspondance est par défaut très souple : tout chevauchement renvoie l'élément. Vous pouvez restreindre la correspondance aux éléments dont les dates sont entièrement englobées par votre date de recherche en préfixant celle-ci d'un « # ». Ex. `#May 10 2005`.

## Rechercher sur des longueurs et largeurs

Pour rechercher sur une longueur ou une largeur, restreignez votre recherche à un élément de longueur ou de largeur et utilisez la quantité voulue avec son unité. Vous **devez** préciser l'unité — il n'y a pas de valeur par défaut, quelle que soit votre préférence d'unité de mesure (cette préférence ne régit que l'affichage). Pour trouver les éléments correspondant exactement à une mesure, recherchez simplement la quantité. CollectiveAccess convertit la quantité dans les unités requises pour la comparaison : même si un élément a été mesuré en pouces, une recherche métrique le trouvera — si les mesures correspondent bien sûr.

```
ca_objects.width:12in
```

Vous pouvez utiliser presque toutes les abréviations d'unités listées sur la page des formats de saisie de mesure. Quelques-unes, comme `"` pour les pouces et `'` pour les pieds, ont une signification particulière dans la syntaxe Lucene et ne doivent pas être utilisées.

Pour rechercher des éléments dans une plage de mesures, indiquez les bornes inférieure et supérieure avec leurs unités. Les valeurs de bornes doivent être séparées par le mot « to » et entourées de crochets. Ne mettez pas d'espace entre la quantité et l'unité. Par exemple :

```
ca_objects.width:[12in to 24in]
```

trouverait tous les objets dont la largeur est comprise entre 12 et 24 pouces (inclus).

## Rechercher sur des nombres

La recherche sur des nombres est très semblable à celle sur des mesures, sauf qu'aucune unité n'est nécessaire. Pour rechercher sur un élément de type entier ou décimal, restreignez votre recherche à l'élément et indiquez le nombre, seul ou en plage. Par exemple, pour trouver les objets ayant une valeur `user_ranking` de 5 :

```
ca_objects.user_ranking:5
```

Pour trouver les objets dont `user_ranking` est compris entre 1 et 5 (inclus) :

```
ca_objects.user_ranking:[1 to 5]
```

## Rechercher sur une devise

La recherche sur une devise est très semblable à celle sur des nombres, sauf qu'un type de devise est requis. Restreignez votre recherche à l'élément de devise et indiquez le montant, seul ou en plage. Le montant doit être préfixé par un code de devise à trois lettres (ex. `EUR` pour les euros, `USD` pour les dollars américains) ou l'un des symboles pris en charge (`$`, `¥`, `£` et `€`). Par exemple, pour trouver les objets dont la valeur `appraisal_value` est de 500 $ :

```
ca_objects.appraisal_value:$500
```

Pour trouver les objets dont `appraisal_value` est inférieure ou égale à 500 $ :

```
ca_objects.appraisal_value:[$0 to $500]
```

## Rechercher sur des localisations géographiques

Pour rechercher sur des localisations géographiques, vous avez deux options. Vous pouvez rechercher dans une boîte englobante définie par deux paires latitude/longitude, ou rechercher tout ce qui se trouve à une distance donnée d'un point latitude/longitude.

Pour rechercher dans une boîte englobante :

```
ca_objects.georeference:"[40.341,-71.011 to 45.322, -75.963]"
```

Les latitudes et longitudes doivent être décimales et séparées par « to », « - » ou « .. » ; l'ensemble de la plage doit être entouré à la fois de crochets (`[` et `]`) et de guillemets. Sans guillemets, la partie de la requête jusqu'au premier espace serait analysée comme géographique — ce que vous ne voulez pas.

Pour rechercher la zone située dans un rayon donné autour d'un point :

```
ca_objects.georeference:"[40.5759250,-73.9911350 ~ 5km]"
```

Comme pour la requête en boîte englobante, entourez l'expression de recherche de crochets et de guillemets. La distance maximale au point peut être exprimée dans n'importe quelle unité de longueur prise en charge par le type d'attribut « Length ». La requête ci-dessus trouvera tout ce qui est géocodé dans un rayon de 5 kilomètres autour du point.

## Rechercher les valeurs vides

Depuis la version 1.4, vous pouvez rechercher les éléments sans contenu dans un champ précis à l'aide du terme spécial `[BLANK]`. `[BLANK]` doit être utilisé conjointement à une spécification de champ et entouré de guillemets doubles. L'exemple suivant renverra tous les objets dépourvus de description :

```
ca_objects.description:"[BLANK]"
```

!!! tip "Complément idéesculture"
    Dans une interface en français, `[VIDE]` est accepté en plus de `[BLANK]`.

## Rechercher les valeurs renseignées

*Section ajoutée par idéesculture : ce terme n'est pas décrit dans la documentation amont, mais il est présent dans le code de Providence au moins depuis la version 1.7.8.*

Le terme spécial `[SET]` fait l'inverse de `[BLANK]` : il renvoie les enregistrements qui ont au moins une valeur dans le champ indiqué. Comme `[BLANK]`, il s'utilise avec une spécification de champ et entre guillemets doubles.

Ce terme est traduit selon la langue de l'interface et **seule la forme traduite est reconnue**. Dans une interface en français, tapez `[DEFINI]` (sans accent) : `[SET]` n'y fonctionne pas. L'exemple suivant renvoie tous les objets qui ont une description :

```
ca_objects.description:"[DEFINI]"
```

## Points d'accès

Taper `ca_objects.description:graffiti` chaque fois que vous voulez chercher le mot « graffiti » dans l'élément « description » devient vite fastidieux, et n'est guère élégant. Pour simplifier la formulation des recherches limitées à un champ ou un élément, CollectiveAccess permet de définir des **points d'accès**. Un point d'accès est simplement une liste de spécifications de champs et d'éléments, définie dans le fichier `search_indexing.conf`, dont le nom peut remplacer la spécification réelle. Par exemple, vous pourriez faire la recherche « description » ainsi :

```
picText:graffiti
```

en supposant qu'un point d'accès comme celui-ci soit défini dans `search_indexing.conf` :

```
picText = {
    fields = [ca_objects.description]
},
```

## Combinaison booléenne

Les expressions de recherche peuvent être combinées avec les opérateurs booléens standard `AND` et `OR`. Joignez simplement vos expressions de recherche avec les mots `AND` et `OR`. Par exemple, la requête

```
ca_objects.appraisal_value:[$0 to $500] AND ca_objects.description:broken
```

trouvera tous les objets ayant À LA FOIS une valeur d'estimation inférieure ou égale à 500 $ et le mot « broken » dans leur description. À l'inverse, la requête

```
ca_objects.appraisal_value:[$0 to $500] OR ca_objects.description:broken
```

trouvera les objets ayant SOIT une valeur d'estimation inférieure ou égale à 500 $, SOIT le mot « broken » dans leur description.

Si vous omettez `AND`/`OR` entre deux expressions de recherche, `AND` est supposé.

!!! tip "Complément idéesculture"
    Le moteur SqlSearch (moteur par défaut) gère aussi :

    - l'exclusion, avec `NOT` ou le signe `-` accolé au terme : `statue NOT bronze` ou `statue -bronze` renvoient les enregistrements qui contiennent « statue » mais pas « bronze » ;
    - le regroupement entre parenthèses : `(statue OR buste) AND marbre` ;
    - la recherche d'une expression exacte entre guillemets doubles : `"statue équestre"` ne renvoie que les enregistrements où ces mots se suivent, dans cet ordre.

    Placez l'exclusion après au moins un terme positif : une requête qui commence par `NOT` renvoie tous les enregistrements sauf ceux qui correspondent au terme exclu. La recherche floue (`~`) et la pondération (`^`) de la syntaxe Lucene ne sont pas prises en charge par SqlSearch.

## Jokers

L'astérisque (`*`) sert de caractère joker : il correspond à n'importe quel texte. Les jokers ne peuvent être utilisés qu'à la fin d'un mot, pour trouver les mots commençant par votre terme de recherche. Par exemple :

```
wri*
```

trouverait les enregistrements associés à des mots commençant par « wri ». Notez que si votre installation a la racinisation (*stemming*) activée, de nombreux mots anglais verront automatiquement leurs suffixes tronqués et un joker ajouté. Ainsi, avec la racinisation, une requête sur « baking », « baked » ou « baker » serait transformée en « bak* ». Le raciniseur est assez intelligent pour ne pas tronquer un terme auquel vous avez vous-même ajouté un joker : si vous recherchez « bake* », il le laisse tel quel.

!!! tip "Complément idéesculture"
    Le raciniseur de SqlSearch, le moteur par défaut, repose sur l'algorithme Snowball **anglais**. La documentation amont de `search.conf` indique qu'il donne de mauvais résultats sur des contenus non anglophones et conseille de le désactiver dans ce cas (`search_sql_search_do_stemming = 0`). Si une recherche en français renvoie des résultats inattendus, faites vérifier ce réglage par votre administrateur.

## Rechercher sur les dates de création et de modification

Vous pouvez rechercher sur les dates de création et de modification des enregistrements à l'aide des points d'accès spéciaux `created` et `modified`, accompagnés d'une expression de date/heure valide. Par exemple, pour trouver tout ce qui a été créé le 12 avril 2012 :

```
created:"April 12 2012"
```

ou

```
created:"4/12/2012"
```

ou toute autre expression de date/heure valide. Toute plage fonctionne, y compris celles précisant l'heure ou définies par mois ou par année.

Vous pouvez limiter les éléments renvoyés à ceux créés ou modifiés par un utilisateur précis en ajoutant un nom d'utilisateur valide après le point d'accès. Par exemple, pour trouver ce qui a été modifié par l'utilisateur « catherine » en avril 2012 :

```
modified.catherine:"4/2012"
```

Notez que le nom d'utilisateur est séparé du point d'accès par un point (« . »), et qu'il s'agit du nom de connexion de l'utilisateur, pas de son nom complet.

!!! tip "Complément idéesculture : interface en français"
    - Les dates sont interprétées dans la langue de l'interface de l'utilisateur. En français, une date numérique se lit jour/mois/année : `created:"12/04/2012"` désigne le 12 avril 2012, alors que `created:"4/12/2012"` désigne le 4 décembre 2012. Les noms de mois s'écrivent en français : `created:"avril 2012"` fonctionne, alors que `created:"April 12 2012"` (exemple ci-dessus) ne renvoie aucun résultat.
    - Les points d'accès traduits `créé` et `modifié` sont acceptés en plus de `created` et `modified` : `modifié.catherine:"avril 2012"`.
    - Pour une plage, utilisez `entre … et …` ou un tiret entouré d'espaces : `modified:"entre 01/03/2026 et 31/03/2026"` ou `modified:"01/03/2026 - 31/03/2026"`. Évitez `du … au …` : le parseur de dates français supprime le mot « au », qu'il traite comme un article, et la plage n'est pas reconnue.
    - Les mots `hier` et `aujourd'hui` sont reconnus : `modified.catherine:"aujourd'hui"`.
    - Les jokers (`*`) sont ignorés dans ces requêtes.

## Rechercher sur des décomptes

Depuis la version 1.7, il est possible d'indexer pour la recherche le nombre de relations et de valeurs répétées par élément de métadonnée. Pour les relations, les décomptes peuvent être ventilés par type de relation, par type d'élément lié, ou les deux. Les requêtes sur décompte sont utiles pour repérer les enregistrements dépourvus de relations spécifiques (ex. trouver les objets sans entité liée comme artiste) ou présentant des problèmes potentiels (ex. trouver les objets ayant entre 10 et 100 entités liées).

Par défaut, l'indexation des décomptes n'est activée que sur les relations objet-entité, ventilées par type de relation. Vous pouvez configurer l'indexation d'autres décomptes dans `search_indexing.conf`.

Les décomptes de relations s'interrogent avec le nom de la table de relation suivi du champ spécial `count`. Par exemple, dans une recherche d'objets, pour trouver tous les objets liés à exactement une entité :

```
ca_objects_x_entities.count:1
```

Pour trouver tous les objets liés à exactement une entité par le type de relation « artist » :

```
ca_objects_x_entities.count/artist:1
```

Pour trouver tous les objets sans entité « artist » liée :

```
ca_objects_x_entities.count/artist:0
```

Pour trouver tous les objets ayant entre 2 et 10 entités liées :

```
ca_objects_x_entities.count:[2 to 10]
```

Et pour trouver tous les objets ayant entre 2 et 10 entités « artist » liées :

```
ca_objects_x_entities.count/artist:[2 to 10]
```

Notez que le nom de table utilisé dans ces exemples est `ca_objects_x_entities` et non `ca_entities`. Quand `ca_objects_x_entities` est indexé avec `count` dans `search_indexing.conf` (c'est le cas par défaut), les décomptes sont ventilés par type de relation, ce qui permet les requêtes sur décompte par type de relation.

Vous pouvez aussi indexer les décomptes sur l'enregistrement lié lui-même (ici `ca_entities`), en les ventilant par type d'enregistrement. En supposant votre système configuré avec les types d'entité « individual » et « organization », ces requêtes seraient possibles.

Trouver les objets ayant des organisations liées :

```
ca_entities.count/organization:[1 to 100000]
```

Trouver les objets n'ayant que des individus liés :

```
ca_entities.count/individual:[1 to 100000] and ca_entities.count/organization:0
```

On utilise ici une plage de borne supérieure 100000 pour inclure les objets ayant un nombre quelconque d'entités. Les expressions avec `<` et `>` ne sont pas prises en charge actuellement.

De même, le nombre de valeurs présentes pour chaque élément de métadonnée est indexé et interrogeable. C'est utile pour repérer les enregistrements dépourvus de valeur dans un champ, ou en ayant beaucoup. Par exemple.

Pour trouver tous les objets dépourvus d'au moins une valeur dans le champ « dimensions » :

```
ca_objects.dimensions.count:0
```

Pour trouver tous les objets ayant plus de 5 valeurs dans le champ « dimensions » :

```
ca_objects.dimensions.count:[5 to 100000]
```

Comme pour toute autre spécification de champ de recherche, vous pouvez créer des alias plus pratiques pour les décomptes fréquents dans `search_indexing.conf` en créant un point d'accès.

!!! info "Source"
    Traduction de la documentation officielle [CollectiveAccess / Providence](https://providence.readthedocs.io/en/latest/), section *Search & Browse — Search Syntax*. Terminologie alignée sur le fichier de localisation `fr_FR` de l'application.
