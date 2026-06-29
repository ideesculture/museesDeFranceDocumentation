# Lexique de traduction — documentation CollectiveAccess (FR)

Référence terminologique pour traduire la documentation officielle Providence (`collectiveaccess/ProvidenceDocs`) vers le français.

**Source de vérité** : fichier de localisation officiel de l'interface, `app/locale/fr_FR/messages.po` du dépôt `collectiveaccess/providence` (branche `master`). On reprend les libellés réellement affichés dans l'interface française, pour que la doc et l'écran emploient les mêmes mots.

**Règle d'or** : ne jamais inventer un terme « logique ». Si un concept n'a pas d'entrée dans le `.po`, le signaler ici et trancher explicitement avant d'écrire.

## Terminologie validée (issue du .po fr_FR)

| Anglais (doc Providence) | Français retenu | Notes |
|---|---|---|
| Display | **Affichage** | L'objet « Display » de CA. Pluriel : « Affichages ». |
| Display template | **Modèle d'affichage** | ⚠️ jamais « gabarit ». |
| Display list | **Liste d'affichage** | |
| Display code | **Code d'affichage** | identifiant alphanumérique de l'affichage |
| Display format | **Format d'affichage** | formatage d'une *valeur* (date, devise…), ≠ l'objet Affichage |
| Template (générique) | **Modèle** | |
| Expression | **Expression** | |
| Bundle | **Bloc** | « paquet », « lot », « offre groupée » dans le .po sont des incohérences MT — ne pas les reprendre. |
| Set | **Ensemble** | menu « Set Tools » → « Ensembles » |
| Movement | **Mouvement** | |
| Storage location | **Emplacement** (de stockage) | libellé d'interface = « Emplacements » |
| History tracking | **Suivi de l'historique** | localisation / mouvements dans le temps |
| Deaccession | **Sortie de l'inventaire** | |
| Barcode | **Code-barres** | |
| Label (impression) | **Étiquette** | « Print results as labels » → « Imprimer les étiquettes » |
| Label / Preferred label (donnée) | **Label / Label préféré** | le titre/nom porté par un enregistrement (distinct de l'étiquette imprimée) |
| Browse | **Parcourir** | |
| Facet | **Facette** | |
| Relationship | **Relation** | « Add relationship » est parfois rendu « Ajouter un lien » : préférer « relation ». |
| Interstitial (data/element) | **Interstitiel** (donnée / élément) | métadonnée portée par une relation |
| Authority | **Autorité** | |
| List / List item | **Liste** / **Élément de liste** | |
| Metadata element | **Élément de métadonnée** | |
| User interface | **Interface utilisateur** | l'interface de saisie d'un type |
| Screen | **Écran** | un écran de saisie au sein d'une interface |
| Locale | **Locale** | |
| Record | **Enregistrement** | |
| PDF output | **Génération PDF / Sortie PDF** | |
| Loan | **Prêt** | table `ca_loans` |
| Occurrence | **Occurrence** | représente souvent une exposition |
| Movement | **Mouvement** | enregistrement de déplacement |
| Storage location | **Emplacement de stockage** | table `ca_storage_locations` |
| Intrinsic (field) | **(champ) intrinsèque** | champ codé en dur, toujours présent |
| Attribute type | **Type d'attribut** | nature d'un élément de métadonnée |
| Access point | **Point d'accès** | alias de recherche défini dans `search_indexing.conf` |
| Wildcard | **Joker** | l'astérisque `*` |
| Stemming | **Racinisation** | (préciser « *stemming* » entre parenthèses au 1er emploi) |
| Bounding box | **Boîte englobante** | recherche géographique |
| Count | **Décompte / nombre** | recherche sur le nombre de relations/valeurs |
| Primary table | **Table principale** | |
| Deaccession | **Sortie de l'inventaire** | et `is_deaccessioned` = « sorti de l'inventaire » |
| Finding aids | **Instruments de recherche** | contexte archivistique (DACS) |
| Lifespan | **Période de vie** | intrinsèque `lifespan` des entités |

## Conventions de rédaction (rappel charte)

- Un paragraphe = une ligne dans le source `.md` (pas de soft-wrap).
- Listes : un item par ligne.
- Garder les **codes/identifiants techniques en anglais** quand ce sont des valeurs de configuration (`ca_objects`, `preferred_labels`, codes de bundle, etc.) — on traduit le texte explicatif, pas les jetons de syntaxe.
- Admonitions Material (`!!! note`, `!!! warning`) pour les encadrés.

## Arbitrages tranchés

- **Display = « Affichage »**, **Display template = « Modèle d'affichage »** (décision 2026-06-29, alignée sur le `.po` officiel, et non « Formats d'affichage »).
