# 10. Les differents types de champs dans CollectiveAccess

## Qu'est ce qu'un champ

blablabla

### Conteneur (container)
Il contient juste un ensemble de champs

### Texte (text)
Un champ texte permet d'écrire des informations de manière libre

### Liste (List)
Les champs listes forcent la sélection d'un terme précis dans une base prédéfinie
Il existe de multiples types de champs liste pour retrouver le terme souhaité

#### 1) Liste déroulante
Une liste déroulante affiche les choix possibles les uns sous les autres, cliquez sur le champ et les différentes possibilités apparaitront, il ne vous plus qu'à cliquer sur le terme recherché afin de le sélectionner

#### 2) Case a cocher


#### 3) Bouton radio
Une liste en bouton radio affiche l'entièreté de la liste avec un bouton à gauche de chaque terme, 
cliquez sur le bouton correspondant au terme souhaité afin de le sélectionner 

#### 4) Liste à cocher 
Une liste à cocher affiche l'entièreté de la liste avec une case à gauche de chaque terme, 
cliquez sur le(s) bouton(s) correspondant au terme souhaité afin de le sélectionner

**??** on peut choisir plusieurs termes d'une liste d'un coup ??

#### 5) Recherche par auto-complétion
Une recherche par auto-complétion vous propose des termes après que vous ayez écris quelques lettres,
utilisez ce champ comme un champ texte classique jusqu'à ce que vous trouviez votre terme

#### 6) Navigation hiérarchique horizontale
Une navigation hiérarchique horizontale cliquer sur la flèche **>** de certains termes afin de trouver ses sous-termes 
puis cliquez sur le terme de votre choix afin de le sélectionner

Vous pouvez utilisez le champ recherche en bas a droite afin de retrouver plus facilement votre terme 

#### 7) Navigation hiérarchique horizontale avec recherche 
**??** c'est pareil que la recherche par auto-complétion
**??** pareil que nav hiérarchique horizontale aussi

#### 8) Vertical hierarchy browser (upward & downward)
Une navigation verticale fonctionne comme une [liste déroulante](#1-liste-deroulante) mais elle ne montre que les termes principaux, si le terme choisis posséde des sous termes une nouvelle liste déroulante au dessus (upward) ou en dessous (downward) de la précédente avec les sous termes, ce procédé ce répete jusqu'à trouver un terme final

### Date (DateRange)
Les champs date permettent de relier un objet, une personne ou un lieu à une période. 

CollectiveAccess traite les dates et heures sous différents formats :
	- Année : 2015 ; 450 av. J.-C. ; vers 1950 ; il y a 40 millions d’années  
	- Période : 1914 - 1926 ; entre juin 2010 et juillet 2010 ; du 5 janvier 2010 au 15 janvier 2010
	- Mois et Année : Juin 1910 ; 06/1910
	- Date : 6/01/1914 ; 6 janvier 1914, 6/01/14
	- Date avec heures  : 7 juin 1914 à 16h43 ; 7/06/1914
	- Expressions : 
aujourd’hui : CollectiveAccess inscrit la date du jour ; 
hier : CollectiveAccess inscrit la date précédente à la date du jour ; 
demain : CollectiveAccess inscrit la suivant la date du jour 
maintenant : date et heure du jour
décennie : 1990’s ; 199-
siècle : 20e S. ; 19—
\'' - Dates incertaines : vers 1955, vers Juin 1860 : 2 Juillet 1921? ; vers 1950-1956 ; 6/11/???? ; 6/????
\'' - Saison : Été 2010 ; Hiver 2010
\'' - Quart de siècle : 20 Q3 (3e quart du 20e siècle : 1950-1975)

*NB : Le fichier de configuration datetime.conf permet de configurer d’autres dates ou périodes de dates selon vos souhaits. *

### Geocode
les geocode permettent de définir des emplacements ou des zones géographiques en lien avec un objet

Voici les différentes option du géocode :

* +/- : 
* recherche :
* ligne :
* pentagone :
* carré :
* cercle :
* édition :
* suppression :

### Url


### Currency


### Length


### Weight


### TimeCOde


### Integer


### Numeric


### LCSH


### GeoNames


### File
Permet d'ajouter des documents en lien avec votre enregistrement :

- Pour ajouter le document de votre choix, cliquez sur **Choisir un fichier**, sélectionnez dans vos documents l'image que vous souhaitez puis ajoutez la
- **Formats de fichier** : Pour information, les formats courants sont : JPEG, TIFF, MPEG-4, vidéo FLASH, FLV, WAV, AIFF, MP3, PDF **a modifier**

### Media
Permet d'ajouter des média en lien avec votre enregistrement : 

- Pour ajouter le média de votre choix, cliquez sur **Choisir un fichier**, sélectionnez dans vos documents l'image que vous souhaitez puis ajoutez la
- **Formats de fichier** : Pour information, les formats courants sont : JPEG, TIFF, MPEG-4, vidéo FLASH, FLV, WAV, AIFF, MP3, PDF **a modifier**

### Taxonomy


### InformationService


### ObjectRepresentations


### Entities


### Places


### Occurences


### Collections


### StorageLocations


### Loans


### Movements


### Objects


### ObjectLots


### FloorPlan


### Color

