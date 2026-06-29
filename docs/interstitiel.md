# Données interstitielles

Depuis la version 1.4, CollectiveAccess prend en charge les **enregistrements de relation**, aussi appelés enregistrements « interstitiels ». Cette fonction permet aux catalogueurs de décrire une relation au-delà du simple choix d'un type de relation. Supposons par exemple que vous ayez deux entités mariées pendant un certain temps, puis divorcées. L'enregistrement de relation permet d'ajouter une plage de dates, un texte narratif et/ou d'autres éléments de métadonnées de votre choix dans l'interstice entre ces deux individus. Les enregistrements de relation sont entièrement facultatifs et ne sont d'ailleurs accessibles que si une interface utilisateur est définie pour eux. Ils ne se limitent pas aux entités : deux enregistrements quelconques peuvent porter cette description interstitielle, à condition que des métadonnées et une interface utilisateur aient été créées. Parmi les exemples courants de relations susceptibles de nécessiter des métadonnées interstitielles : objets vers lieux, objets vers entités, entités vers lieux, etc.

!!! note "Concept"
    Une donnée **interstitielle** est une métadonnée portée par la relation elle-même, et non par l'un des deux enregistrements liés. Elle vit « entre » les deux enregistrements. C'est le mécanisme qui permet, par exemple, de dater un prêt ou de qualifier le rôle d'une entité dans une relation.

## Modifier les enregistrements de relation

Lorsqu'une relation dispose d'éléments de métadonnées et d'une interface utilisateur dédiés, une petite icône d'édition apparaît sur les relations concernées, après leur premier enregistrement. Cliquer sur cette icône 📎 (un trombone dans l'interface) ouvre l'enregistrement de relation dans une fenêtre en surimpression.

!!! info "Source"
    Traduction de la documentation officielle [CollectiveAccess / Providence](https://providence.readthedocs.io/en/latest/), section *Data Modelling — Interstitial Data*. Terminologie alignée sur le fichier de localisation `fr_FR` de l'application.
