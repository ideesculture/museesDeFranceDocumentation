# Les expressions

Les expressions sont des instructions évaluées par CollectiveAccess en une valeur texte, numérique ou booléenne (`true`/`false`). Elles permettent de déclencher conditionnellement (ou non) des éléments d'une correspondance d'import ou d'un modèle d'affichage, la valeur booléenne renvoyée déterminant ce qui se produit. Les valeurs peuvent être générées par des fonctions (détaillées plus bas), des comparaisons et des opérations mathématiques.

Dans sa forme la plus simple, une expression est une quantité numérique ou textuelle. Voici des exemples d'expressions parfaitement valides :

- `5`
- `"Software is great"`

Vous remarquerez dans les exemples ci-dessus que les nombres ne sont que des nombres, tandis que le texte doit être entouré de guillemets (simples ou doubles). Toute quantité non vide et non nulle est évaluée à `true` : ainsi `5` vaut `true` tandis que `0` vaut `false`. `-1` vaut aussi `true`, car c'est une valeur non nulle. Toute chaîne autre que `""` (aucun texte) vaut `true`, même `" "` (un seul espace).

Si les valeurs uniques sont des expressions valides, elles ne sont généralement utiles qu'en combinaison avec des **opérateurs**. Les opérateurs sont des symboles qui prennent deux opérandes (valeurs), effectuent une opération et renvoient une nouvelle valeur. Plusieurs types d'opérateurs sont disponibles.

## Opérateurs de comparaison

Les opérateurs de comparaison comparent deux opérandes et renvoient `true` ou `false`. Le plus courant est `=`, qui renvoie `true` si les opérandes sont exactement identiques, `false` sinon. Par exemple, `"wood" = "wood"` vaut `true` tandis que `"wood" = "cement"` ne l'est pas. Dans une correspondance d'import, on peut utiliser l'opérateur `=` pour vérifier qu'un champ d'entrée vaut une certaine valeur.

Les autres opérateurs de comparaison sont :

- `>` supérieur à
- `<` inférieur à
- `>=` supérieur ou égal
- `<=` inférieur ou égal
- `<>` différent de
- `!=` différent de (forme alternative)

Les opérateurs supérieur/inférieur ne fonctionnent qu'avec des valeurs numériques. L'égalité et l'inégalité fonctionnent avec des nombres ou du texte.

### Comparaison booléenne

À partir de la version 1.8, les valeurs représentant les booléens `true` et `false` sont utilisables dans les comparaisons. Elles permettent de tester plus facilement la valeur de retour d'une expression ou d'une fonction à l'aide du mot nu, sans guillemets, `true` ou `false`. Par exemple, cette expression :

```none
dateIsRange("1950's") = false
```

renverrait `true` quand `dateIsRange()` renvoie `false`, ce qui est utile pour les actions d'import et les modèles d'affichage où certains comportements sont déclenchés par des expressions vraies.

## Opérateurs mathématiques

Avec les expressions, vous pouvez effectuer des opérations mathématiques sur les nombres à l'aide de `+`, `-`, `*` et `/` (addition, soustraction, multiplication et division). L'opérateur `+` fonctionne aussi sur le texte et fusionne deux valeurs textuelles en une seule. Par exemple :

```none
4 + 5
```

renverra la valeur `9`.

```none
"Julia" + " plus " + "Allison"
```

renverra la valeur `"Julia plus Allison"`.

## Opérateurs logiques

Il est également possible d'enchaîner plusieurs expressions en une expression composite plus grande à l'aide des opérateurs de logique booléenne `AND` et `OR`. `AND` renvoie `true` si, et seulement si, les deux opérandes valent `true`. `OR` renvoie `true` si, et seulement si, au moins un opérande vaut `true`. Par exemple :

```none
(5 > 10) AND ("seth" = "seth")
```

vaut `false`, car 5 n'est pas supérieur à 10 et les deux expressions doivent être vraies pour que le `AND` composite soit vrai.

```none
(5 > 10) OR ("seth" = "seth")
```

vaut `true`, car `"seth" = "seth"` est vrai et il suffit qu'une seule expression le soit pour que le `OR` logique renvoie `true`.

!!! note
    Avant la version 1.8, les opérateurs logiques devaient être en majuscules uniquement. Les deux casses sont désormais autorisées.

## Opérateurs de comparaison supplémentaires

Les opérateurs de comparaison ci-dessus sont utiles mais limités. Deux autres opérateurs sont là où tout se joue.

### L'opérateur `IN`

`IN` permet de comparer une valeur à une liste de valeurs. Il renvoie `true` si N'IMPORTE quelle valeur de la liste correspond à la valeur comparée. Par exemple :

```none
"Seth" IN ["Julia", "Allison", "Sophie", "Maria", "Angie", "Seth"]
```

renvoie `true` tandis que

```none
"Joe" IN ["Julia", "Allison", "Sophie", "Maria", "Angie", "Seth"]
```

renvoie `false`.

Il existe aussi un opérateur `NOT IN` associé, qui renvoie `true` si la valeur n'est pas dans la liste.

### L'opérateur `=~` (expression régulière)

Vous pouvez comparer une valeur à une expression régulière avec l'opérateur `=~`. Les expressions régulières sont une syntaxe de reconnaissance de motifs très puissante et très souple. Dans sa forme la plus simple, une expression régulière est un simple bout de texte recherché n'importe où dans la valeur comparée. Par exemple :

```none
"Software is great" =~ /soft/
```

renvoie `true`.

Notez que l'expression régulière se trouve à droite de l'opérateur et est entourée de caractères `/`. C'est la notation traditionnelle des expressions régulières : elles sont entourées de barres obliques pour les distinguer du texte normal.

Il existe aussi un opérateur `!~` associé, qui renvoie `true` quand la valeur ne correspond pas à l'expression régulière.

## Variables

Tout cela est bien beau, mais les exemples ci-dessus, avec leurs valeurs codées en dur, ne sont pas très utiles. C'est avec les variables que les choses deviennent vraiment intéressantes. Toute source d'un enregistrement d'import peut servir de variable en préfixant son nom d'un caractère `^`. Ainsi, si vous importiez un tableur Excel et vouliez appliquer des règles lorsque le mot « allison » apparaît dans la valeur de la colonne 4, vous écririez :

```none
^4 =~ /allison/
```

De même, pour vous assurer que la valeur de la 10e colonne vaut « metal », utilisez l'expression :

```none
^10 = "metal"
```

Pour vous assurer que les deux conditions s'appliquent à un enregistrement, utilisez :

```none
(^4 =~ /allison/) AND (^10 = "metal")
```

Si l'une ou l'autre suffit, utilisez `OR` plutôt que `AND`.

Pour les données XML en entrée, les noms de variables sont les chemins XML — exactement ce qui est utilisé dans la spécification de source, mais avec un `^` ajouté devant.

## Fonctions

Les fonctions sont des boîtes noires dans lesquelles vous mettez un certain nombre de valeurs pour en ressortir une seule. Le système d'expressions propose actuellement les fonctions suivantes :

| Fonction | Description |
|---|---|
| `abs` | Renvoie la valeur absolue d'un nombre (transforme les nombres négatifs en positifs) ; prend une seule valeur. |
| `ceil` | Arrondit un nombre fractionnaire à l'entier supérieur ; prend une seule valeur. |
| `floor` | Arrondit un nombre fractionnaire à l'entier inférieur ; prend une seule valeur. |
| `int` | Force un nombre à être entier. La partie décimale est supprimée ; prend une seule valeur. |
| `max` | Renvoie la plus grande des valeurs passées ; prend un nombre quelconque de valeurs. |
| `min` | Renvoie la plus petite des valeurs passées ; prend un nombre quelconque de valeurs. |
| `round` | Arrondit le nombre à l'entier le plus proche ; prend une seule valeur. |
| `random` | Renvoie un nombre aléatoire entre zéro et le nombre fourni ; prend une seule valeur. |
| `rand` | Synonyme de `random`. |
| `current` | Vaut `true` si l'expression de date fournie englobe la date/heure actuelle du serveur (v1.5). |
| `future` | Vaut `true` si l'expression de date fournie *se termine* après la date/heure actuelle du serveur. La date de début n'est pas considérée (v1.5). |
| `wc` | Renvoie le nombre de mots (*word count*) d'une valeur texte fournie (v1.5). |
| `length` | Renvoie le nombre de caractères d'une valeur texte fournie (v1.5). |
| `sizeof` | Renvoie le nombre de paramètres. Utile pour compter des valeurs (v1.6). |
| `count` | Synonyme de `sizeof`. |
| `age` | Calcule l'âge en années. Accepte un nombre quelconque de paramètres (> 1). Prend la date la plus ancienne et la plus récente comme début et fin de l'intervalle, l'ordre importe peu. Si le résultat est un intervalle de 0 an (parce qu'une seule date a été passée), il réessaie en ajoutant la date courante — utile pour calculer l'âge actuel de quelque chose ou de quelqu'un (v1.6). |
| `ageyears` | Alias de `age` (v1.6). |
| `agedays` | Comme `age`/`ageyears`, mais en jours (v1.6). |
| `avgdays` | Calcule la durée moyenne des intervalles passés en paramètres. Accepte un nombre quelconque de paramètres (> 1) (v1.6). |
| `formatdate` | Formate une expression de date valide avec la fonction `date()` de PHP. Format ISO par défaut ; accepte un second paramètre facultatif précisant le format (v1.6). |
| `formatgmdate` | Formate une expression de date valide en UTC avec la fonction `gmdate()` de PHP. Format ISO par défaut ; accepte un second paramètre facultatif (v1.6). |
| `isvaliddate` | Renvoie `true` si le paramètre s'analyse comme une date valide (v1.7). |
| `date` | Analyse une date en langage naturel en une paire d'horodatages historiques, adaptés à la comparaison mathématique. |
| `join` | Renvoie une liste de valeurs délimitées par le premier argument ; les autres arguments sont les valeurs. Alias `implode` (v1.7). |
| `implode` | Synonyme de `join`. |
| `trim` | Supprime les espaces de début et de fin d'une chaîne (v1.7). |
| `avg` | Renvoie la moyenne des valeurs en paramètres. |
| `sum` | Renvoie la somme des valeurs en paramètres. |
| `replace` | Remplace des valeurs à l'aide d'une expression régulière (compatible Perl ; valeur de remplacement ; valeur sujet). |
| `idnoUseCount` | Renvoie le nombre d'éléments pour lesquels une valeur est utilisée comme identifiant (`idno`) dans une table donnée (table facultative, `ca_objects` par défaut). |
| `dateIsRange` | Renvoie `true` si la date est une plage plutôt qu'un jour, un mois ou une année unique (v1.8). |
| `fromUnixtime` | Convertit un horodatage Unix en date au format ISO-8601 (v1.8). |

Pour inclure la valeur produite par une fonction dans votre expression, ajoutez simplement le nom de la fonction suivi d'une liste de valeurs entre parenthèses. Par exemple :

```none
random(10) > 5
```

renvoie `true` si le nombre aléatoire entre 0 et 10 est supérieur à 5.

- `ceil(5.2)` renvoie 6
- `floor(5.6)` renvoie 5
- `round(5.2)` renvoie 5
- `round(5.6)` renvoie 6
- `length("hello")` renvoie 5
- `sizeof(1,2,3,4)` renvoie 4
- `age("23 June 1912", "7 June 1954")` renvoie 41
- `age("7 June 1954", "23 June 1912")` renvoie 41 (l'ordre n'importe pas)
- `age("7 June 1954", "9 May 1945", "23 June 1912")` renvoie 41 (les dates « en trop » n'importent pas)
- `age("28 January 1985")` renvoie une valeur > 29 ; 30 si on l'exécute avant le 28 janvier 2016
- `agedays("23 June 1912", "7 June 1954")` renvoie 15324
- `agedays("1912/06/23")` renvoie une valeur > 37653
- `avgdays("1912/06/23 - 1954/06/07", "1985/01/28 - 2015/07/24")` renvoie 13229
- `avgdays("1945/01/02 - 1945/01/03", "1985/01/28 - 1985/01/29")` renvoie 1
- `trim(" ce texte a des espaces à la fin   ")` renvoie « ce texte a des espaces à la fin »
- `join(", ", "Smith", "Bob")` renvoie « Smith, Bob »

!!! note
    Les fonctions `formatdate` et `formatgmdate` peuvent renvoyer des résultats variables selon le réglage de fuseau horaire défini dans `setup.php`.

## Parenthèses

Vous avez peut-être remarqué que des parenthèses parsèment certains exemples. Vous pouvez utiliser des parenthèses appariées pour regrouper des éléments d'une expression. Cela en facilite la lecture et garantit que les opérateurs sont appliqués dans l'ordre voulu dans les expressions complexes. Trois choses à retenir : (1) chaque sous-expression parenthésée est évaluée comme une unité avant d'être combinée aux autres ; (2) chaque parenthèse ouvrante doit toujours être appariée à une parenthèse fermante ; (3) les parenthèses ne nuisent à rien et améliorent la lisibilité, vous êtes donc encouragé à en user généreusement.
