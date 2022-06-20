# 7. La saisie d’un objet dans CollectiveAccess

	Nous abordons dans ce chapitre les points suivants :

		- la démarche de saisie 
		- le panorama des écrans de saisie
		- les liens entre les objets et les entités, collections, thésaurus... 
		- l’association d’un un média à un objet 

		CollectiveAccess est une application multi-langue, vous pouvez répéter les métadonnées pour les saisir dans toutes les langues souhaitez.

## Qu’entend par objet ?

Les objets correspondent aux éléments que vous gérez. 
Vous pouvez diversifier votre collection en définissant des types d'objets.

Par exemple, le profil de Saisie Joconde (créé à partir des recommandations du Service des Musées de France) définit différents types d'objets dans deux grandes catégories d’objets :

- les biens affectés : collections propres de l’établissement 
- les biens déposés : objets prêtés ou déposés par d’autres établissements

La liste des types d’objets est définie et paramètre selon vos collections, vous pouvez l’enrichir ou la modifier depuis le menu Gérer de CollectiveAccess. (*cette fonctionnalité est détaillée dans le support administration de CollectiveAccess*).

## Comment créer un objet ?
Pour créer un objet  :

- lors de la saisie d’un objet lié, si celui-ci n’est pas déjà présent dans la base, CollectiveAccess vous propose de le créer au fil de l’eau. L'objet nouvellement crée alimente directement le fichier des objets.

Sinon :

- cliquez sur le menu « Nouveau » dans la barre de navigation principale.
- sélectionnez « Objet » dans le menu déroulant, puis choisissez un type (Bien affecté, bien déposé) pour créer un nouvel enregistrement.
*NB : la liste des types d'objets dépend de votre paramétrage. (cf. support de cours administration de CollectiveAccess)*

## Tour des différents écrans de saisie

L'éditeur d'objets comprend par défaut onze écrans contenant les champs d'informations nécessaires à la création d’un nouvel objet :

- [les informations de base (Identification)](#identifier-lobjet)
- [la description du bien](#description-du-bien)
- [le contexte historique](#contexte-historique)
- [le statut juridique](#statut-juridique)
- [les informations complémentaires](#informations-complémentaires)
- [Saisie Joconde]()**??**
- [les informations concernant les médias](#media)
- [les relations liées à l'objet](#relations)
- [les droits d'accès](#droits-dacces)
- [le résumé](#resume)
- [les logs](#les-logs)

## Quelques conseils de saisie

Nous vous conseillons d’enregistrer vos modifications avant de passer à l'écran suivant, dans le cas contraire, une alerte vous demandera de confirmer que vous voulez quitter l’écran en cours sans enregistrer.

##### Enregistrer / Annuler / Supprimer
Pour enregistrer/annuler votre saisie ou supprimer votre objet, cliquez sur les boutons du même nom qui se trouvent en haut et en bas de votre écran de saisie.

##### Définir plusieurs valeurs 
Si vous avez besoin de définir plus d’une valeur pour un des champs affichés à l’écran, cliquez sur le + en bas du champ.

## Détail de la saisie écran par écran

*NB : les écrans et les métadonnées décrits correspondent à ceux mis en place au sein du profil Joconde et répondent aux spécifications du Service des Musées de France*
*Les interfaces de saisie et les métadonnées sont modifiées en fonction de vos besoins et de votre fonctionnement ; nous décrivons ces fonctionnalités dans les supports de cours administration.*

L'écran "Saisie Joconde" reprend les écrans "Identification", "Description du bien", "Contexte historique", "Statut juridique" et "Informations complémentaires". Pour y accéder directement donnez un [N° d'inventaire](#n-dinventaire) à l'objet, [enregistrez](#enregistrer-annuler-supprimer) puis cliquez sur **Saisie Joconde** à gauche.

### Identifier l'objet
Contient les informations les plus élémentaires pour enregistrer un nouvel objet.

#### N° d’inventaire
Saisissez un identifiant alphanumérique en respectant les règles de saisies définies au sein de votre établissement.[Texte](../types_de_champs/#texte-text)

#### Autre numéro (ancien numéro?)
[Texte](../types_de_champs/#texte-text) : Saisissez les autres numéros de référence de l’objet ; vous pouvez saisir plusieurs autres numéros.

#### Domaine
Trouver le domaine de l'objet grâce à un [champ auto-completif](../types_de_champs/#5-recherche-par-auto-completion)
ou recherchez dans le thesaurus le domaine souhaité.

*Lien vers le thesaurus :* ￼*https://opentheso.huma-num.fr/opentheso/?idt=th294*￼

#### Dénomination
Saisissez ici la désignation (le nom commun de l'objet) utilisée pour votre objet.
[Champ auto-completif](../types_de_champs/#5-recherche-par-auto-completion)
**affixe**

#### Appelation
Saisissez ici toute autre désignation utilisée pour votre objet.
L'appelation correspond souvent à la désignation de l'objet à son époque
[Texte](../types_de_champs/#texte-text)

#### Titre de l'oeuvre  
Correspond au nom de l'objet. [Texte](../types_de_champs/#texte-text)
_Attention ce champ est obligatoire : si l'objet ne possède pas de titre ou de position, vous pouvez saisir son identifiant._

* #### Auteur, exécutant, collecteur
Saisissez ici le nom du producteur de l’objet. Ce champ est directement lié aux enregistrements « [entités](./Saisie_Entite) » :

- saisissez quelques lettres (au moins 3) et CollectiveAccess vous propose toutes les entités dont le nom commence par ces lettres, vous pouvez ensuite le sélectionner;
- si l’auteur saisi n’existe, une fenêtre pop-up vous permet de le créer directement depuis la saisie de l’objet et l’ajoute directement au fichier des entités.
- choissisez si l'entité lié à l'objet en est **l'auteur** , **le collecteur** ou **l'exécutant** grâce à la liste à coté après avoir chosi l'auteur

#### Ecole
Indiquez dans ce champ **??**

Recherchez le style de l’objet dans le thesaurus du Service des Musées de France Style / Ecole.

*Lien vers le thesaurus : https://opentheso.huma-num.fr/opentheso/?idt=th295*￼

#### Anciennes attributions
[Texte](../types_de_champs/#texte-text) : Correspond aux informations sur le(s) ancien(s) possesseur(s) de l'objet

#### Période de création/exécution
[Champ auto-completif](../types_de_champs/#5-recherche-par-auto-completion)
Recherchez la période de production de l'objet (si connu) grâce à un [menu arborescent]()

#### Millésime de création/exécution 
[Date](../types_de_champs/#date-daterange) de production précise de l'objet (si connu). 

#### Époque, styles
Rentrez ici l'époque, le style et le mouvement de l'objet grâce à un [champ auto-complétif]()
deux affixe sont disponibles afin de préciser où ce place l'objet durant l'époque, le style ou le mouvement 

### Description du bien
Contient les informations du physique de l'objet

#### Matériaux et techniques
[Champ auto-completif](../types_de_champs/#5-recherche-par-auto-completion)
Vous permet d’associer un ou plusieurs couple de matériaux et techniques à l’objet en les recherchant dans le thesaurus matériaux et techniques fourni par le Service des Musées de France.

*Lien vers le thesaurus :*￼*https://opentheso.huma-num.fr/opentheso/?idt=th291*

#### Dimensions
Saisissez ici les dimensions connues de l’objet : diamètre, profondeur, hauteur, poids ainsi que sa largeur. Indiquez l’unité de mesure à la suite de la valeur.

CollectiveAccess intègre la gestion de toutes les unités de mesures et  les convertit lors des recherches effectuées.
Le champ "Type de dimensions" vous permet de préciser le type de mesure ou la partie mésurée si l'objet est complexe

*Lien vers la documentation du SMF :*￼*http://www.culture.gouv.fr/documentation/joconde/fr/partenaires/AIDEMUSEES/methode.htm#DIMS*

#### Marques et inscriptions (inventaire) 
Détaillez dans ce champ les marques et inscriptions que vous pouvez relever sur l’objet en précisant les informations suivantes :

- Alphabet ([Texte](../types_de_champs/#texte-text)) : Notifiez ici l'alphabet dans lequel l'inscription est écrite
- Emplacement de l’inscription ([Texte](../types_de_champs/#texte-text)) : Où est placée l'inscription sur l'objet
- Langue ([Texte](../types_de_champs/#texte-text)) : La langue dans laquelle est écrite l'inscription
- Transcription de l’inscription ([Texte](../types_de_champs/#texte-text)) : Grâce à un éditeur de texte enrichi, vous pouvez retranscrire au plus précis le sens de l'inscription
- Type d’inscription ([menu arborescent]()) : Recherchez dans ce menu le type d'inscription ou de marque correspondant à celui de l'objet

#### Onomastique
Ce champ sert à préciser les noms propres (de personnages, d'auteurs, de lieux,...) liés à l'objet

#### Description
Au sein de ce champ au format [texte]() enrichi, saisissez une description détaillée de votre objet

#### État du bien au moment de l'acquisition ou du dépot
Rentrez ici la constatation d'état de l'objet au moment de l'acquisition ou du dépot

#### Constat d’état
Décrivez le constat d’état initial de l’objet : date du constat, constat d'état, état global et commentaire ; vous pouvez associer à ce constat tout document numérique souhaité.

#### Représentation (décor)
Si l'objet répresente quelque chose indiquez ici le genre de la répresentation de l'objet ainsi que jusq'à 6 termes pour mieux définir la répresentation. un champ précision et aussi disponible en bas afin de **???**

*https://opentheso.huma-num.fr/opentheso/?idt=th285*

Trouvez la bonne représentation de l'objet grâce à un [champ auto-completif](../types_de_champs/#5-recherche-par-auto-completion)

#### Précision sur la représentation
[Champ textuel]() afin d'apporter des précisions sur la représentation

#### Date de la représentation
Date de naissance et/ou de mort des personnages de la représentation ou date de l'évenement représenté (année/mois/jour)

#### Source de la représentation
Indiquez ici les œuvres de réferences de la répresentation :
- Genre : le type d'œuvre de réference  
- Nature : **??**
- Nom de l'auteur : l'auteur de l'œuvre de réference 
- Titre de l'oeuvre : le titre de l'œuvre de réference
- Précisions : précisions concernant l'œuvre

*https://opentheso.huma-num.fr/opentheso/?idt=th286*

### Contexte historique

#### Genèse
La genèse de l'objet est composée de 3 champs :

- Stade de création : ce champ indique l'étape de production de l'objet ainsi que s'il est/à une reproduction 
- Contexte : le contexte de la création de l'objet (commande, pièce d'essai,...)
- Objet associé : indiquez ici s'il existe un objet ou un œuvre en lien avec l'objet décrit (vous préciserais l'objet en question dans le champ d'en dessous)

https://opentheso.huma-num.fr/opentheso/?idt=th298

#### Objet(s) associé(s)
[Champ auto-completif](../types_de_champs/#5-recherche-par-auto-completion) :
Lié au fichier des objets.
Vous pouvez lier des objets à l’objet que vous décrivez.
Si l'objet n'existe pas vous pouvez le créer

#### Historique
Champ texte vous permettant de décrire le contexte historique de l’objet

#### Lieu de création/d'exécution
Recherchez le lieu grâce a un [menu arborescent]().
Sélectionnez si le lieu est de celui de la création/de l'éxécution de l'objet, celui de la production de l'objet ou celui de la publication de l'objet en bas a droite après avoir choisi le lieu
Si le lieu n'existe pas vous pouvez [le créer]()

#### Précisions sur les lieux de création/d'exécution
Précisions sur le(s) lieu(x)

#### Géographie historique
Champ vous permettant de préciser le nom des lieux au moment de la création de l'objet

#### Utilisation/destination
Réferez vous au thesaurus afin de trouver le(s) terme(s) qui correspond(ent) le mieux à l'utilisation/la destination de l'objet

*Lien vers le thesaurus : https://opentheso.huma-num.fr/opentheso/?idt=th304*

#### Précisions sur l'utilisation/destination
Précisions sur le(s) utilisation(s)/destination(s)

#### Lieu(x) d'utilisation, destination
Recherchez le lieu grâce à un [menu arborescent]().
Si le lieu n'existe pas vous pouvez [le créer]()

#### Précisions sur les lieux d'utlisation/destination
Précisions sur le(s) lieu(x)

#### Période d'utilisation/destination
Période à laquelle l'objet est utilisé (précison maximum de 25 ans)
Choisissez la période de destination de l'objet grâce à un [menu arborescent]()

#### Millésime d'utilisation/destination
Période à laquelle l'objet est utilisé (Année précise)

### Pour les objets issue de fouille/trouvaille archéologique

#### Lieu de découverte, de collecte ou de récolte
Lien vers le fichier des lieux, sélectionnez un lieu dans le [menu arborescent]() et précisez s’il s’agit d’un lieu d’utilisation / destination , de création, de découverte ou de récolte en bas à droite

*Lien vers le thesaurus : https://opentheso.huma-num.fr/opentheso/?idt=th284*

#### Type de site de découverte
Type de site dans lequel l'objet à été découvert
Choisissez le type de site de découverte de l'objet grâce à un [champ auto-completif](../types_de_champs/#5-recherche-par-auto-completion)

*Lien vers le thesaurus : https://opentheso.huma-num.fr/opentheso/?idt=th292*

#### Méthode de découverte, collecte, ou de récolte d’un objet
Précisez la méthode utilisée lors de la découverte, de la collecte ou de la récolte d’un objet.

*Lien vers le thesaurus : https://opentheso.huma-num.fr/opentheso/?idt=th292*

#### Date de découverte, collecte, récolte
Indiquez la date de la découverte, de la collecte ou de la récolte de l’objet (précision maximum au jour près).
le champ "Type de date" sert à préciser si la date est une date de découverte ou de collecte
*Lien vers la documentation du SMF : ￼http://www.culture.gouv.fr/documentation/joconde/fr/partenaires/AIDEMUSEES/methode.htm#DATEDECV￼*

#### Découvreur
Champ **pas** lié au fichier des entités, saisissez ici le nom du découvreur.

#### Précisions sur la découverte 
Précisions sur la découverte, la collecte ou la récolte de l'objet

#### Numéro du site SDA
Précisez ici le numéro du site SDA duquel est issu l'objet

### Statut juridique

#### Date d'inscrption au registre de l'inventaire
**Je comprend pas la diff avec Date d’affectation au musée** 

#### Type de propriété
Indiquez le type de propriété de l’objet parmi les choix disponibles dans la [liste déroulante]()

#### Mode d’acquisition
Choisissez dans la [liste déroulante]() le mode d’acquisition de l’objet .
*Lien vers la documentation du SMF : ￼http://www.culture.gouv.fr/documentation/joconde/fr/partenaires/AIDEMUSEES/methode.htm#ACQU￼*

#### Prix d'achat en euros
Cette case indique le prix d'achat (soit tous les frais liés à l'achat) ou la valeur donnée par des experts du bien.le prix doit être en euros(€)
*ne mettez pas d'espaces entre les chiffres (ex : 140 000 n'est pas valide, entrez 140000). Pour préciser les centimes utiliser une virgule et non un point (ex : 140,000 au lieu de 140.000)*

#### Mention des concours publics
Indiquez ici s’il s’agit d’une acquisition subventionnée par l'État ou une collectivité publique ou non
*Lien vers la documentation du SMF : ￼http://www.culture.gouv.fr/documentation/joconde/fr/partenaires/AIDEMUSEES/methode.htm#MENTION￼*

#### Etablissement affectataire
Ce champ est lié au fichier des [entités](), saisissez l’établissement affectataire de l'objet dans ce [champ auto-complétif]().

#### Date et références de l’acte d’acquisition
Saisissez la [date]() et la référence de l’acte d’acquisition.
Vous pouvez donner des précisions sur la date si dans la [liste déroulante]() à gauche de date 
*Lien vers la documentation du SMF : ￼http://www.culture.gouv.fr/documentation/joconde/fr/partenaires/AIDEMUSEES/methode.htm#DACQ￼*

#### Date d’affectation au musée
Saisissez la [date] à laquelle l'objet à été affecté au musée. Utlisez la [liste déroulante]() à gauche pour apporter des précisions sur la liste
*Lien vers la documentation du SMF : ￼http://www.culture.gouv.fr/documentation/joconde/fr/partenaires/AIDEMUSEES/methode.htm#DAFF￼*

#### Avis des instances scientifiques compétentes
Pour chaque avis, précisez quelle instance scientifique l’a donné, son sens (favorable / défavorable), sa date ; une zone « commentaires » vous permet de le détailler.
*Lien vers la documentation du SMF : ￼http://www.culture.gouv.fr/documentation/joconde/fr/partenaires/AIDEMUSEES/methode.htm#AVIS￼*

#### Anciennes appartenances
Champ texte qui vous permet de détailler les anciennes appartenances de l’objet.
*Lien vers la documentation du SMF : ￼http://www.culture.gouv.fr/documentation/joconde/fr/partenaires/AIDEMUSEES/methode.htm#APTN￼*

#### Anciens Dépots
Champ texte qui permet de noter dans quel(s) dépot(s) à déja été entreposé l'objet

### Informations complémentaires

#### Exposition
Champ texte permettant de préciser les expositions dans lesquelles l’objet a été exposé ; les expositions actuelles sont décrites dans une fiche Exposition reliée à l’objet.

#### Bibliographie
Champ de texte enrichi dans lequel vous pouvez saisir une note du publication

#### Commentaires
Saisissez ici toutes les informations que vous n’avez pu saisir ailleurs qu’il s’agisse des informations liées à la conservation de l’objet ou à son contexte d’acquisition.

#### Crédits photographiques
Champ texte enrichi dans lequel vous pouvez saisir les crédits de photographies utilisée(s)

#### Rédacteur
Rédacteur de la notice : **plus** relié au fichier des entités

### Média 
Permet d'ajouter une ou plusieurs images(s) en lien avec votre objet

#### Représentations média
Intégrer une image grâce à ce champ :

- Écrivez dans label préféré le nom que voous voulez donner à votre image
- Sélectionner si l'image est de face ou de dos dans type **??** 
- Définissez l'accessibilité de l'image dans la liste déroulante "Accès"
- Vous pouvez définir un statut pour la représentation si vous attendez modifications ou si vous les avez réalisées

#### Crédits photographiques
Champ texte enrichi dans lequel vous pouvez saisir les crédits de photographies utilisée(s)

### Relations
Cet écran récapitule toutes les relations qui lient l'objet aux autres enregistrements de la base : objets, entités,lieux, occurrences, collections.
* lors de création d’une entité (par exemple), la sélection ou la saisie d’un objet ajoute directement l’objet en tant qu’objet lié de l’entité
* vous pouvez également saisir le lien entre un objet et un enregistrement directement depuis cet écran : dans le champ recherche, indiquez l’identifiant de l’enregistrement ou son nom :
	- la saisie d’au moins trois caractères dans la case de recherche vous propose une liste d’enregistrements contenant ces caractères,
	    - sélectionnez ensuite l’enregistrement souhaité.
	    - définissez le type de lien entre les deux enregistrements
	    - enregistrez : la nouvelle relation apparaît dans la fiche de l'objet et sera également affichée dans l’enregistrement (objet, entité…) lié.
La croix (x) située à droite d'une relation vous permet de la supprimer.
Si l’enregistrement recherché n’apparaît pas dans la liste déroulante, n’ayant pas encore été créé dans la base, CollectiveAccess vous donne la possibilité de le créer à la volée.

### Droits d'accès

#### Accès
Définissez l'accessibilité de l'objet pour le public

#### Conditions d'accès
Les conditions d'accès 

### Résumé
L’écran Résumé récapitule les informations saisies dans la fiche entité, selon le format d’affichage sélectionné dans le menu déroulant présent en haut à droite de l’écran à coté de button 
vous permettant de télécharger le résumé de l'enregistrement en pdf.[^1]

[^1]:Vous pouvez créer de nouveaux formats d’affichages en allant dans le menu Gérer \> Mes affichages. (cf. Support administration de CollectiveAccess, gestion des formats d’affichages).
Si le menu et le bouton ne sont pas présents c'est qu'aucun n'affichage n'as été crée.

### Les logs
Les logs correspondent à l'historique de l’enregistrement.
Cet écran présente tous les changements apportés à l’enregistrement et indique l’identifiant de l’utilisateur ayant effectué ces modifications, la nouvelle valeur mise en place, ainsi que la date et l’heure correspondant à la modification.

[Pdf](/pdf/methode_redaction_informatisee_notices._20210211.pdf)

