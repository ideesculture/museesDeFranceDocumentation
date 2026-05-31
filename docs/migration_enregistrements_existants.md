# Gestion des enregistrements déjà présents (conflits à l'import)

Les règles relatives aux enregistrements existants sont une option de la section Paramètres d'une feuille de calcul de correspondance d'import de données. 

Il existe plusieurs règles à choisir lors de l'établissement d'une correspondance, et ces règles déterminent comment les enregistrements qui se trouvent déjà dans un système CollectiveAccess sont traités et vérifiés par rapport aux données sources importées. Bien qu'il existe une politique pour un système CollectiveAccess qui n'a pas d'enregistrements importés(vide), la plupart des imports se font dans des bases ayant déjà des enregistrements. 

A noter, il n'est possible de définir qu'un unique comportement pour la gestion des enregistrements déjà présents. Il n'est pas possible de spécifier que dans un cas on doublonne, dans un autre on dédoublonne, dans un troisième cas on ignore ; tout cela au sein d'une même feuille d'import.

## Remarque

Pour comprendre les règles relatives aux enregistrements existants et leur signification, il est utile de savoir que dans CollectiveAccess, le champ d'identification principal de chaque enregistrement est "idno" (numéro d'identification), tandis que le champ principal du titre/nom est "preferred_label" (étiquette préférée).

Les politiques relatives aux enregistrements existants déterminent la manière dont les enregistrements créés par la correspondance d'import sont intégrés, fusionnés ou séparés des autres enregistrements existants. Ces règles sont conçues pour être utilisées dans les importations de données qui contiennent plusieurs parties ou, en d'autres termes, qui utilisent plusieurs correspondances d'importation. En outre, ces règles peuvent être utilisées lors de la révision d'une feuille de calcul de correspondance d'import. Toutes les règles relatives aux enregistrements existants disponibles depuis la version 1.8 de CollectiveAccess sont définies ci-dessous.

## Quand utiliser chaque politique d'enregistrement existante ?
Il est utile de réfléchir à la nature exacte des données représentées dans une correspondance d'importation et, le cas échéant, aux données déjà importées dans le système CollectiveAccess.

Il est également utile d'envisager le contexte plus large de la façon dont les données sources seront représentées dans CollectiveAccess. Cela peut parfois s'avérer difficile, car la feuille de correspondance d'import n'est qu'un tableau de concordance et n'est pas censée représenter l'aspect réel des données sources une fois importées dans un système CollectiveAccess.

Voici quelques questions utiles à se poser lors du choix d'une politique d'enregistrement existant :

- Ai-je déjà des données importées dans mon système CollectiveAccess ?

- Quel type de données est déjà importé, le cas échéant ?

- Quel type de données est représenté dans mes données sources et dans la correspondance d'importation subséquente ? (Ceci peut être vu dans le paramètre " Tableau ").

- Comment ces données doivent-elles interagir avec les autres données que j'ai déjà importées ?

## Politiques relatives aux enregistrements existants

### none

Un système CollectiveAccess est " vide ", c'est-à-dire qu'il ne contient aucune autre donnée importée. Il n'est pas nécessaire de définir des règles relatives aux enregistrements existants, car il n'y a pas d'enregistrements existants dans le système. Pour les importations comportant plusieurs parties, ce paramètre s'applique souvent à la toute première importation de données.

### skip_on_idno

Ignorer si déjà présent dans la base.

### merge_on_idno

Les enregistrements de la feuille de calcul de correspondance des importations seront fusionnés avec tous les enregistrements existants dans le système CollectiveAccess sur la base d'un numéro d'enregistrement partagé ou d'un numéro d'identification d'un enregistrement.

### merge_on_idno_with_replace
Les enregistrements de la feuille de calcul de la correspondance d'importation seront fusionnés avec tous les enregistrements existants dans le système CollectiveAccess sur la base d'un numéro d'enregistrement partagé ou du numéro d'identification d'un enregistrement. En outre, les enregistrements spécifiés dans la correspondance d'import qui partagent un numéro d'identification avec des enregistrements du système remplaceront ceux qui existent déjà dans le système CollectiveAccess.

### overwrite_on_idno

Si déjà présent dans la base, l'enregistrement existant est écrasé.

### skip_on_preferred_labels
### merge_on_preferred_labels

Les enregistrements de la feuille de calcul de la correspondance importée seront fusionnés avec tous les enregistrements existants dans le système CollectiveAccess en fonction du titre ou du nom d'un enregistrement.

### merge_on_preferred_labels_with_replace
Les enregistrements de la feuille de calcul de la correspondance importée seront fusionnés avec tous les enregistrements existants dans le système CollectiveAccess par correspondance avec le titre ou le nom partagé d'un enregistrement, ou son étiquette_préférée. En outre, les enregistrements spécifiés dans la correspondance d'import qui partagent des titres ou des noms avec des enregistrements du système remplaceront ceux qui existent déjà dans le système CollectiveAccess.

### overwrite_on_preferred_labels
### skip_on_idno_and_preferred_labels
### merge_on_idno_and_preferred_labels

Les enregistrements de la feuille de calcul de correspondance importée seront fusionnés avec tous les enregistrements existants dans le système CollectiveAccess sur la base d'un numéro d'identification partagé et d'une étiquette préférée partagée.

### merge_on_idno_with_preferred_labels_with_replace
### overwrite_on_idno_and_preferred_labels