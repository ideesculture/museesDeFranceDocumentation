# 9. La saisie des lieux dans CollectiveAccess
CollectiveAccess vous propose une gestion des lieux sous la forme d’une [arborescence (hiérarchie)](), deux possibilités s’offrent à vous :

- nous pouvons importer une arborescence de lieux si vous nous sollicitez ou dans le cadre de votre marché
- vous pouvez créer une arborescence de lieux directement depuis Providence, ou modifier l’arborescence importée le cas échéant.
## Qu’entend-on par lieux ?
La position de votre enregistrement dans la hiérarchie est indiquée en haut de chaque écran.
*(Exemple de chemin : commune \> quartier \> rue).*
Vous pouvez également afficher à tout instant ces informations en sélectionnant « montrer les informations hiérarchiques » dans l'explorateur.
Deux menus déroulants dans ce menu vous permettent de créer des enregistrements enfants, frères et sœurs.
## Comment créer un nouveau lieu
* Dans la barre de navigation principale sélectionnez Nouveau \> Lieu.
* Accéder au niveau de [l'arborescence]() où vous souhaitez enregistrer la nouvelle autorité. 
* Sélectionnez le dossier (terme) parent[^1]. Le chemin du nouvel enregistrement s'affiche directement au dessus.

[^1]:Pour sélectionnez un terme cliquez sur **>** correspondant, cliquer sur le nom vous amènera sur les pages de modification du lieu. 

* Ensuite sélectionnez le type de lieu que vous souhaitez ajouter dans le [menu déroulant](). Ces types de lieu sont configurables dans l'éditeur de listes. 
* Cliquez sur le + pour créer un nouveau lieu qui sera pris en compte dans l'éditeur.

## Sélecteur hiérarchique
Le sélecteur hiérarchique s'ouvre automatiquement sur les écrans d'informations(basique ou supplémentaire).
Ce sélecteur vous permet de consulter la place du lieu dans l'arborescence, Cliquez sur un lieu ou sur *Afficher dans le navigateur* pour ouvrir l'arborescence complète.

## Description des écrans de saisie
Les lieux contiennent les informations suivantes sur votre collection :

- [les informations de base](#information-basique)
- [les informations supplémentaire](#information-supplementaire)
- [les relations liées au lieu](#relations)
- [les liens avec d'autres sites](#liens)
- [le résumé](#resume)
- [les logs](#les-logs)

### Information basique
Cet écran contient les informations nécessaires à un nouvel enregistrement.

#### Labels préférés
Nommez le nouveau lieu.

#### Identifiant du lieu 
Attribuez un identifiant (code) au lieu.

#### Notes (usage interne seulement)
Si besoin, décrivez plus précisément le lieu créé.

### Relations
Cet écran récapitule toutes les relations qui lient le lieu aux autres enregistrements de la base : objets, entités,lieux, occurrences, collections.

* lors de création d’un objet (par exemple), la sélection ou la saisie d’un lieu ajoute directement l’objet en tant qu’objet lié du lieu

* vous pouvez également saisir le lien entre un lieu et un enregistrement directement depuis cet écran : dans le champ recherche, indiquez l’identifiant de l’enregistrement ou son nom :
	- la saisie d’au moins trois caractères dans la case de recherche vous propose une liste d’enregistrements contenant ces caractères,
	    - sélectionnez ensuite l’enregistrement souhaité.
	    - définissez le type de lien entre les deux enregistrements
	    - enregistrez : la nouvelle relation apparaît dans la fiche de l'entité et sera également affichée dans l’enregistrement (objet, entité…) lié.
		
La croix (x) située à droite d'une relation vous permet de la supprimer.

Si l’enregistrement recherché n’apparaît pas dans la liste déroulante, n’ayant pas encore été créé dans la base, CollectiveAccess vous donne la possibilité de le créer à la volée.

### Liens
Vous pouvez relier le lieu à un (ou plusieurs) site(s) web(s)

* Nom du site web : Donner le nom du site du lieu
* Url : Donner le lien pour accéder au site du lieu

### Résumé
L’écran Résumé récapitule les informations saisies dans la fiche entité, selon le format d’affichage sélectionné dans le menu déroulant présent en haut à droite de l’écran à coté de bouton 
vous permettant de télécharger le résumé de l'enregistrement en pdf.[^2]

[^2]:Vous pouvez créer de nouveaux formats d’affichages en allant dans le menu Gérer \> Mes affichages. (cf. Support administration de CollectiveAccess, gestion des formats d’affichages).
Si le menu et le bouton ne sont pas présents c'est qu'aucun affichage n'as été crée.

### Les logs
Les logs correspondent à l'historique de l’enregistrement.
Cet écran présente tous les changements apportés à l’enregistrement et indique l’identifiant de l’utilisateur ayant effectué ces modifications, la nouvelle valeur mise en place, ainsi que la date et l’heure correspondant à la modification.



