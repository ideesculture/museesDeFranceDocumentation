# 1. Présentation de la Saisie Joconde 

Cette page vous permet de découvrir les fonctionnalités présents pour chacunes des 6 procédures qui seront décrites par la suite.

### Enregistrements Principaux
Il existe 3 types d'enregistrements importants pour réaliser une saisie Joconde:

- [Les Objets]()
- [Les Entités]()
- [Les Lieux]()

Ces 3 enregistrementds permettent de définir très précisement une œuvre.

## Quelques conseils de saisie

Nous vous conseillons d’enregistrer vos modifications avant de passer à l'écran suivant, dans le cas contraire, une alerte vous demandera de confirmer que vous voulez quitter l’écran en cours sans enregistrer.

##### Menu gauche 
Lors de la saisie d'un enregistrement (objet,entité,lieu, etc..) vous trouverez à gauche un menu avec plusieurs utilités :

- Surveiller l'enregisrement : cliquez sur l'œil pour "surveiller" l'objet, une fois l'enregistrement surveillé vous pourrez ajouter un widget dans votre tableau de bord afin d'avoir un raccourci vers l'objet
- Modifier le type : Si vous créez un enregistrement avec le mauvais type vous pourrez le remplacer par un autre type facilement (par exemple un objet en bien affecté au lieu de bien déposé)
- Dupliquer l'enregistrement : Si vous avez à créer plusieurs enregistrement similaire vous pouvez dupliquer un enregistrement et modifier les différences entre les enregistrements
- Informations Supplémentaires : cliquez sur le *i* pour afficher la date de création et la date de la dèrnier modification de l'enregistrement.

Vous pouvez aussi sélectionner l'écran que vous souhaitez modifiez depuis ce menu.

##### Enregistrer / Annuler / Supprimer
Pour enregistrer/annuler votre saisie ou supprimer votre objet, cliquez sur les boutons du même nom qui se trouvent en haut et en bas de votre écran de saisie.

##### Définir plusieurs valeurs 
Si vous avez besoin de définir plus d’une valeur pour un des champs affichés à l’écran, cliquez sur le + en bas du champ.

### Les Écrans de base
Les Écrans décrits ici sont présents (à la base) sur toutes les saisies (d'objets, de lieux, d'entités, etc..)

#### Relations
Cet écran récapitule toutes les relations qui lient le lieu aux autres enregistrements de la base : objets, entités,lieux, occurrences, collections.

* lors de création d’un objet (par exemple), la sélection ou la saisie d’un lieu ajoute directement l’objet en tant qu’objet lié du lieu

* vous pouvez également saisir le lien entre un lieu et un enregistrement directement depuis cet écran : dans le champ recherche, indiquez l’identifiant de l’enregistrement ou son nom :
	- la saisie d’au moins trois caractères dans la case de recherche vous propose une liste d’enregistrements contenant ces caractères,
	    - sélectionnez ensuite l’enregistrement souhaité.
	    - définissez le type de lien entre les deux enregistrements
	    - enregistrez : la nouvelle relation apparaît dans la fiche de l'entité et sera également affichée dans l’enregistrement (objet, entité…) lié.
		
La croix (x) située à droite d'une relation vous permet de la supprimer.

Si l’enregistrement recherché n’apparaît pas dans la liste déroulante, n’ayant pas encore été créé dans la base, CollectiveAccess vous donne la possibilité de le créer à la volée.

#### Résumé
L’écran Résumé récapitule les informations saisies dans la fiche de l'enregistrement selon le format d’affichage sélectionné dans le menu déroulant présent en haut à droite de l’écran à coté de bouton 
vous permettant de télécharger le résumé de l'enregistrement en pdf.[^1]

[^1]:Vous pouvez créer de nouveaux formats d’affichages en allant dans le menu Gérer \> Mes affichages. (cf. Support administration de CollectiveAccess, gestion des formats d’affichages).
Si le menu et le bouton ne sont pas présents c'est qu'aucun affichage n'as été crée.

#### Les logs
Les logs correspondent à l'historique de l’enregistrement.
Cet écran présente tous les changements apportés à l’enregistrement et indique l’identifiant de l’utilisateur ayant effectué ces modifications, la nouvelle valeur mise en place, ainsi que la date et l’heure correspondant à la modification.

## Types de champs
CollectiveAccess ce sert de champ afin de recupérer les informations, voici les principaux types que vous rencontrerez.

#### Texte (text)
Un champ texte permet d'écrire des informations de manière libre

#### Liste (List)
Les champs listes forcent la sélection d'un terme précis dans une base prédéfinie. Les Listes sont consultables, modifiables et ajoutables en vous rendant dans Gérer \> Listes et vocabulaires.

Il existe de multiples types de champs liste pour retrouver le terme souhaité

##### 1) Liste déroulante
Une liste déroulante affiche les choix possibles les uns sous les autres, cliquez sur le champ et les différentes possibilités apparaitront, il ne vous plus qu'à cliquer sur le terme recherché afin de le sélectionner

##### 2) Liste à cocher / Boutons radio
Une liste à cocher affiche l'entièreté de la liste avec une case à gauche de chaque terme, 
cliquez sur le(s) bouton(s) correspondant au terme souhaité afin de le sélectionner

La différence entre une liste à cocher et des boutons radio est le nombre de choix possibles, vous ne pouvez sélectionner qu'un terme pour des boutons radioconrairement la liste à cocher ou vous pouvez en sélectionner autant que vous le souhaitez.[^2]
[^2]:Les coches des listes à cocher sont carrées et celles des boutons radios sont rondes

##### 3) Recherche par auto-complétion
Une recherche par auto-complétion vous propose des termes après que vous ayez écris quelques lettres,
utilisez ce champ comme un champ texte classique jusqu'à ce que vous trouviez votre terme

##### 4) Navigation hiérarchique horizontale
Une navigation hiérarchique horizontale cliquer sur la flèche **>** de certains termes afin de trouver ses sous-termes 
puis cliquez sur le terme de votre choix afin de le sélectionner

Vous pouvez utilisez le champ recherche en bas à droite afin de retrouver plus facilement votre terme 

##### 6) Navigation Verticale (Vertical hierarchy browser (upward & downward))
Une navigation verticale fonctionne comme une [liste déroulante](#1-liste-deroulante) mais elle ne montre que les termes principaux, si le terme choisis posséde des sous termes une nouvelle liste déroulante au dessus (upward) ou en dessous (downward) de la précédente avec les sous termes, ce procédé ce répete jusqu'à trouver un terme final

#### Date (DateRange)
Les champs date permettent de relier un objet, une personne ou un lieu à une période. 

CollectiveAccess traite les dates et heures sous différents formats :

- Année : 2015 ; 450 av. J.-C. ; vers 1950 ; il y a 40 millions d’années  
- Période : 1914 - 1926 ; entre juin 2010 et juillet 2010 ; du 5 janvier 2010 au 15 janvier 2010
- Mois et Année : Juin 1910 ; 06/1910
- Date : 6/01/1914 ; 6 janvier 1914, 6/01/14
- Date avec heures  : 7 juin 1914 à 16h43 ; 7/06/1914
- Expressions : 

	- aujourd’hui : CollectiveAccess inscrit la date du jour 
	- hier : CollectiveAccess inscrit la date précédente à la date du jour 
	- demain : CollectiveAccess inscrit la suivant la date du jour 
	- maintenant : date et heure du jour
	- décennie : 1990’s ; 199-
	- siècle : 19e S. ; 19—
	- Dates incertaines : vers 1955, vers Juin 1860 : 2 Juillet 1921? ; vers 1950-1956 ; 6/11/???? ; 6/????
	- Saison : Été 2010 ; Hiver 2010
	- Quart de siècle : 20 Q3 (3e quart du 20e siècle : 1950-1975)


