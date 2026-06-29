# Les unités `<unit>`

La balise `<unit>` est l'outil clé pour mettre en forme des données répétables, hiérarchiques ou issues d'enregistrements liés. Ce chapitre complète la [syntaxe des modèles d'affichage](affichage_modeles.md) avec des exemples détaillés.

## Conteneurs répétables

Pour inclure un conteneur répétable dans un affichage, vous devez utiliser la balise `<unit>`. Sans balises `<unit>`, un conteneur d'adresse répétable ressemblerait à ceci :

```text
Ligne d'adresse 1 A; Ligne d'adresse 1 B
Ligne d'adresse 2 A; Ligne d'adresse 2 B
Ligne d'adresse 3 A; Ligne d'adresse 3 B
```

alors que nous voudrions évidemment qu'il ressemble à ceci :

```text
Ligne d'adresse 1 A
Ligne d'adresse 2 A
Ligne d'adresse 3 A
Ligne d'adresse 1 B
Ligne d'adresse 2 B
Ligne d'adresse 3 B
```

Pour obtenir la disposition idéale ci-dessus, une balise `<unit>` sert à définir le format de chaque bloc distinct, qui se répète ensuite autant de fois que le conteneur.

Supposons que vous remontiez cette adresse dans un bloc « Entités liées », afin d'afficher l'adresse avec le nom de l'entité. Le modèle d'affichage ressemblerait à ceci :

```xml
<unit relativeTo="ca_entities">
<unit><l>^ca_entities.preferred_labels</l><br/><br/></unit>
<unit relativeTo="ca_entities.address" delimiter=", ">
^ca_entities.address.address1<ifdef code="ca_entities.address.address2">, </ifdef>
^ca_entities.address.address2<ifdef code="ca_entities.address.city">, </ifdef>
^ca_entities.address.city<ifdef code="ca_entities.address.stateprovince">, </ifdef>
^ca_entities.address.stateprovince<ifdef code="ca_entities.address.postalcode">, </ifdef>
^ca_entities.address.postalcode<ifdef code="ca_entities.address.country">, </ifdef>
^ca_entities.address.country</unit>
</unit>
```

Dans le code ci-dessus, le séparateur d'unité (`,`) est utilisé entre les occurrences du conteneur d'adresse complet. Le code `<ifdef>` est utilisé entre les lignes de chaque adresse individuelle. Il garantit qu'en l'absence de données cataloguées, vous n'obtiendrez pas une suite d'espaces vides et de virgules.

## Relativement aux relations

La balise `<unit>` prend également en charge le réglage `relativeTo`, qui sert à déplacer le cadre de référence d'un affichage vers une cible précise. C'est essentiel pour les affichages d'enregistrements interstitiels, les affichages hiérarchiques et les relations indirectes (voir ci-dessous).

## Relations hiérarchiques

La balise `<unit>` permet d'organiser et d'afficher les métadonnées d'enregistrements liés hiérarchiquement. Par exemple, vous pourriez avoir une hiérarchie dans la table Collections, où une collection parente abrite des collections enfants plus petites. Sans la balise `<unit>`, vous ne pourriez afficher que le label préféré de chaque enfant, sans pouvoir préciser de séparateurs tels que des retours à la ligne. Avec la balise `<unit>`, en revanche, vous pouvez découper les enregistrements enfants en blocs distincts et inclure des métadonnées supplémentaires sur chacun. Pour afficher les enregistrements enfants avec leur `idno`, par exemple, vous pourriez faire ceci :

```xml
<unit relativeTo="ca_collections.children">^ca_collections.preferred_labels,
   ^ca_collections.idno</unit>
```

où `relativeTo` indique la table concernée et demande à l'affichage de trouver les enregistrements enfants. Une fois le cadre `relativeTo` défini, vous pouvez toutefois abandonner le `.children` et simplement référencer la table Collections, où vivent les enregistrements enfants. Si vous continuiez à inclure `children` (c.-à-d. `ca_collections.children.preferred_labels`), vous chercheriez en réalité des enfants au sein des enfants. Pour utiliser ce modèle dans l'autre sens, afficher le parent immédiat de l'enregistrement, formatez-le simplement en `<unit relativeTo="ca_collections.parent">`. Pour afficher tous les parents, formatez le modèle par rapport à la hiérarchie entière : `<unit relativeTo="ca_collections.hierarchy">`. Si vous manipulez plusieurs enregistrements, en tant qu'enfants (`children`) ou que hiérarchie (`hierarchy`), vous voudrez encadrer tout le modèle dans une `<unit>`, afin que les métadonnées de chaque enregistrement soient affichées de façon organisée. Par exemple :

```xml
<unit>
  <unit relativeTo="ca_collections.children" delimiter="</br>">^ca_collections.preferred_labels,
     ^ca_collections.idno
  </unit>
</unit>
```

afficherait les enregistrements ainsi :

```text
Mini collection X, 100.1
Mini collection Y, 100.2
```

au lieu de ceci :

```text
Mini collection X, Mini collection Y, 100.1, 100.2
```

Vous pouvez aussi imbriquer des niveaux supplémentaires de balises `<unit>` dans la syntaxe vue ci-dessus, en suivant les indications de la section suivante.

## Relations indirectes

Un usage de la balise `<unit>` est de permettre aux catalogueurs d'afficher des métadonnées à une certaine distance relationnelle de l'enregistrement choisi. On pourrait appeler cela « les six degrés de séparation de Kevin Bacon pour CollectiveAccess ».

Supposons que vous créiez une synthèse de Collection et que vous souhaitiez afficher des métadonnées sur des Entités, mais que les Entités ne soient pas liées directement aux Collections. Peut-être sont-elles liées à des Objets eux-mêmes liés à la Collection. Pas d'inquiétude : tout comme certaines célébrités sont à deux degrés de Kevin Bacon, les Entités sont aussi à deux degrés des Collections grâce à leur relativité aux Objets.

Comment cela se présente-t-il en pratique ? Voici un modèle d'affichage utilisé sur le bloc objet (via l'interface graphique) ou sur l'emplacement objet (dans un profil). Il remonte des métadonnées de mention depuis un conteneur de chaque fiche Entité liée à chaque Objet :

```xml
<unit relativeTo="ca_objects">
<unit><em><strong>^ca_objects.preferred_labels</strong></em><br></unit>
<unit relativeTo="ca_entities" delimiter=", ">^ca_entities.preferred_labels</unit><br>
<unit relativeTo="ca_entities.statement" delimiter="<br/><br/>">
^ca_entities.statement.statement_text<br/>
^ca_entities.statement.statement_date<br/>
^ca_entities.statement.statement_source</unit>
</unit><br/><br/>
```

Le résultat est une liste de titres d'œuvres, de noms d'artistes et de leurs mentions pour les œuvres de la collection. Notez que dans l'exemple Falling Water, l'entité John Smith comporte deux occurrences du conteneur de mention.

## Relations indirectes restreintes

Vous pouvez restreindre davantage les relations indirectes en incluant `restrictToTypes` et/ou `restrictToRelationshipTypes`. Par exemple, pour restreindre la relation incluse dans l'affichage aux seules entités `individual` liées comme `artist`, utilisez ceci :

```xml
<unit relativeTo="ca_objects">
<unit><em><strong>^ca_objects.preferred_labels</strong></em><br></unit>
<unit relativeTo="ca_entities" delimiter=", "
     restrictToRelationshipTypes="artist" restrictToTypes="ind">
        ^ca_entities.preferred_labels</unit>
<br/><br/>
```

## Tri

Vous pouvez trier l'ordre de sortie des unités en ajoutant `sort` et, facultativement, `sortDirection` à l'unité. Par exemple, pour trier la sortie par le nom de l'objet lié :

```xml
<unit relativeTo="ca_objects" sort="ca_objects.preferred_labels.name" sortDirection="ASC">
<unit><em><strong>^ca_objects.preferred_labels</strong></em><br></unit>
<unit relativeTo="ca_entities" delimiter=", "
   restrictToRelationshipTypes="artist" restrictToTypes="ind">
      ^ca_entities.preferred_labels
</unit><br/><br/>
```

Notez que le sens de tri est `ASC`. Le sens peut être `ASC` (croissant) ou `DESC` (décroissant). Si vous omettez la valeur, le tri croissant est supposé. Vous pouvez trier sur plusieurs valeurs de bloc en listant chacune à la suite, séparées par des points-virgules.

## Ignorer des unités

(À partir de la v1.5) Vous pouvez ignorer des enregistrements sélectionnés par les balises d'unité à l'aide de l'attribut `skipIfExpression`. Il prend une [expression](affichage_expressions.md) en paramètre. Notez que `skipIfExpression` est évalué au niveau de l'enregistrement : vous pouvez l'utiliser même si votre spécification `relativeTo` est un conteneur ou un attribut, mais cela n'a alors guère de sens. Voici un exemple simple qui ignorerait toutes les entités dont l'`idno` contient la séquence `test` :

```xml
<unit relativeTo="ca_entities" delimiter=" / " skipIfExpression="^ca_entities.idno =~ /test/">
    ^ca_entities.preferred_labels
</unit>
```
