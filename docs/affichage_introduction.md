# Affichages et modèles d'affichage

Un **affichage** dans CollectiveAccess est une présentation configurable des données d'un enregistrement : il définit quels blocs (champs de métadonnées) sont restitués, dans quel ordre et sous quelle forme. Les affichages servent à l'écran (fiches, colonnes des résultats de recherche), dans les éditions et exports, et dans les thèmes du site public Pawtucket.

Le cœur d'un affichage est le **modèle d'affichage** (*display template*) : un texte mêlant du contenu fixe et des marqueurs `^` remplacés par les valeurs de l'enregistrement. Maîtriser cette syntaxe permet de produire des fiches lisibles, des étiquettes, des colonnes d'export sur mesure, et d'aller chercher des données portées par les enregistrements liés.

!!! note "Terminologie"
    On parle d'**affichage** (l'objet « Display » de CollectiveAccess) et de **modèle d'affichage** (« Display template »), conformément aux libellés de l'interface française. Le terme « gabarit » n'est pas employé.

Cette section traduit et adapte la documentation officielle Providence. Elle se compose de :

- **[Syntaxe des modèles d'affichage](affichage_modeles.md)** — les marqueurs, les options, les conditions, l'accès aux données liées.
- **[Les unités `<unit>`](affichage_unites.md)** — formater les conteneurs répétables, les hiérarchies et les relations indirectes.
- **[Les expressions](affichage_expressions.md)** — calculs, comparaisons et fonctions utilisables dans les conditions et les modèles.

!!! info "Source"
    Traduction de la documentation officielle [CollectiveAccess / Providence](https://providence.readthedocs.io/en/latest/), section *Reporting*. La terminologie suit le fichier de localisation `fr_FR` de l'application.
