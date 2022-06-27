# 7. La saisie d’un objet dans CollectiveAccess

Nous abordons dans ce chapitre les points suivants :

- la démarche de saisie 
- le panorama des écrans de saisie 
- les liens entre les objets et les entités, collections, thésaurus... 
- l’association d’un un média à un objet 

CollectiveAccess est une application multi-langue, vous pouvez répéter les métadonnées pour les saisir dans toutes les langues souhaitez.

## Qu’entend-t-on par objet ?

Les objets correspondent aux éléments que vous gérez. 
Vous pouvez diversifier votre collection en définissant des types d'objets.

Par exemple, le profil de saisie Joconde (créé à partir des recommandations du Service des Musées de France) définit différents types d'objets dans deux grandes catégories d’objets :

- les biens affectés : collections propres de l’établissement 
- les biens déposés : objets prêtés ou déposés par d’autres établissements

Nous retrouvons ainsi les types d’objets suivants :

- beaux-arts
- dessin
- numérique
- peinture
- photographie
- imprimé
- sculpture

La liste des types d’objets est définie et paramètre selon vos collections, vous pouvez l’enrichir ou la modifier depuis le menu Gérer de CollectiveAccess. (*cette fonctionnalité est détaillée dans le support administration de CollectiveAccess*).

## Tour des différents écrans de saisie

L'éditeur d'objets comprend par défaut huit écrans contenant les champs d'informations nécessaires à la création d’un nouvel objet :

- les informations de base
- les informations administratives
- les informations concernant les médias
- les informations de conservation et de stockage
- les informations fixes
- les relations liées à l'objet
- les mots-clés
- les informations de connexion
- le résumé

## Détail de la saisie écran par écran

*NB : les écrans et les métadonnées décrits correspondent à ceux mis en place au sein du profil Joconde et répondent aux spécifications du Service des Musées de France*
*Les interfaces de saisie et les métadonnées sont modifiées en fonction de vos besoins et de votre fonctionnement ; nous décrivons ces fonctionnalités dans les supports de cours administration.*

### Les informations de base

Contient les informations les plus élémentaires pour enregistrer un nouvel objet.

Nom de la collection

* **N° d’inventaire** :  saisissez un identifiant alphanumérique en respectant les règles de saisies définies au sein de votre établissement.

* **Autre numéro** : saisissez les autres numéros de référence de l’objet en indiquant un type d’autre numéro (fiche cartonnée musée, inventaire fort…) ; vous pouvez saisir plusieurs autres numéros.

* **Domaine** : recherchez dans le thesaurus fourni par le Service des Musées de France le domaine souhaité.

*Lien vers la documentation du SMF :* ￼*http://www.culture.gouv.fr/documentation/joconde/fr/partenaires/AIDEMUSEES/methode.htm#DOMN*￼

* **Désignation principale** : correspond au nom de l'objet.
*Attention ce champ est obligatoire : si l'objet ne possède pas de titre ou de position, vous pouvez saisir son identifiant.*

* **Autres désignations** (libellés non préférés) : saisissez ici toute autre désignation utilisée pour votre objet ; et sélectionnez le type de désignation correspondant dans le menu déroulant « type ».

La sélection du type « utiliser pour » permettra à CollectiveAcces d'identifier votre objet par cette désignation qui ne sera jamais affichée comme un autre titre. 

Vous pouvez ajouter autant d’appellations ou dénominations que nécessaire en cliquant sur le +.

* **Auteur, exécutant ** : saisissez ici le nom du producteur de l’objet. Ce champ est directement lié aux enregistrements « entités » :
	- saisissez quelques lettres et CollectiveAccess vous propose toutes les entités dont le nom commence par ces lettres, vous pouvez ensuite le sélectionner;
	- si l’auteur saisi n’existe, une fenêtre pop-up vous permet de le créer directement depuis la saisie de l’objet et l’ajoute directement au fichier des entités.

* **Ecole** : recherchez le style de l’objet dans le thesaurus du Service des Musées de France Style / Ecole.

*Lien vers la documentation du SMF :* ￼*http://www.culture.gouv.fr/documentation/joconde/fr/partenaires/AIDEMUSEES/methode.htm#ECOL*￼

* **Datation précise** : date de production précise de l'objet. CollectiveAccess traite les dates et heures sous différents formats :
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

*NB : Le fichier de configuration datetime.conf permet de configurer d’autres dates ou périodes de dates selon vos souhaits. *

### Description du bien

* **Matériaux / techniques** : vous permet d’associer un ou plusieurs couple de matériaux et techniques l’objet en les recherchant  dans le thesaurus matériaux et techniques fourni par le Service des Musées de France.

*Lien vers la documentation du SMF :*￼*http://www.culture.gouv.fr/documentation/joconde/fr/partenaires/AIDEMUSEES/methode.htm#TECH*￼
* **Dimensions**  : saisissez ici les dimensions connues de l’objet : largeur, hauteur et profondeur ainsi que son poids. Indiquez l’unité de mesure à la suite de la valeur.
	*Exemples :*
	-  Largeur : 6 m ; Hauteur : 3,4 m 
	-  Largeur : 64 cm ; Hauteur : 14 cm
CollectiveAccess intègre la gestion de toutes les unités de mesures et  les convertit lors des recherches effectuées. 
*Lien vers la documentation du SMF :*￼*http://www.culture.gouv.fr/documentation/joconde/fr/partenaires/AIDEMUSEES/methode.htm#DIMS*￼
* **Inscriptions** : détaillez dans ce champ les marques et inscriptions que vous pouvez relever sur l’objet en précisant les informations suivantes : 
	- transcription de l’inscription : grâce à un éditeur de texte enrichi, vous pouvez retranscrire au plus précis
	- type d’inscription
	- emplacement de l’inscription 
	- Langue, emplacement
\*Lien vers la documentation du SMF : ￼http://www.culture.gouv.fr/documentation/joconde/fr/partenaires/AIDEMUSEES/methode.htm#INSC￼
* **Description** : au sein de ce champ au format texte enrichi, saisissez une description détaillée de votre objet
### Statut juridique
* **Type de propriété **: indiquez le type de propriété de l’objet
* **Mode d’acquisition** : saisissez ici le mode d’acquisition de l’objet en ajoutant éventuellement un commentaire.
*Lien vers la documentation du SMF : ￼http://www.culture.gouv.fr/documentation/joconde/fr/partenaires/AIDEMUSEES/methode.htm#ACQU￼*
* **Prix** : indiquez le prix de l’objet suivie de la devise d’origine
Utilisez les symboles $, €, £… ou trois lettres : EUR pour euros, USD pour US Dollars…
*Exemple* : 100 €, 100 EUR ou 100 $ …
* **Valeur d’assurance** : indiquez ici la valeur d’assurance de votre objet ainsi que la date à laquelle celle-ci a été attribuée.
* **Date et références de l’acte d’acquisition** : saisissez la date et la référence de l’acte d’acquisition.
*Lien vers la documentation du SMF : ￼http://www.culture.gouv.fr/documentation/joconde/fr/partenaires/AIDEMUSEES/methode.htm#DACQ￼*
* **Mention des concours publics** : indiquez ici s’il s’agit d’une acquisition subventionnée ou non
*Lien vers la documentation du SMF : ￼http://www.culture.gouv.fr/documentation/joconde/fr/partenaires/AIDEMUSEES/methode.htm#MENTION￼*
* **Propriétaire** : ce champ est lié au fichier des Entités, saisissez le propriétaire de la même manière que vous avez précédemment saisi l’auteur. A savoir, quelques lettres et CollectiveAccess vous propose les entités liées qui correspondent ; si l’entité saisie n’existe pas, vous pouvez la créer au fil de l’eau.
* **Etablissement affectataire** : ce champ est lié au fichier des Entités, saisissez l’établissement affectataire de la même manière que vous avez précédemment saisi l’auteur.
* **Avis des instances scientifiques** : pour chaque avis,  précisez quelle instance scientifique l’a donné, son sens (favorable / défavorable), sa date ; une zone « commentaires » vous permet de le détailler.
*Lien vers la documentation du SMF : ￼http://www.culture.gouv.fr/documentation/joconde/fr/partenaires/AIDEMUSEES/methode.htm#AVIS￼*
* **Date d’affectation au musée** : date d’affectation de l’objet au musée
*Lien vers la documentation du SMF : ￼http://www.culture.gouv.fr/documentation/joconde/fr/partenaires/AIDEMUSEES/methode.htm#DAFF￼*
* **Donateur, testateur, ou vendeur** : champ lié au fichier des entités, saisissez l’entité de la même manière que vous avez précédemment saisi l’auteur et précisez ensuite s’il s’agit d’un donateur, testateur ou vendeur.
*Lien vers la documentation du SMF : ￼http://www.culture.gouv.fr/documentation/joconde/fr/partenaires/AIDEMUSEES/methode.htm#DONA￼*
* **Anciennes appartenances** : champ texte qui vous permet de détailler les anciennes appartenances de l’objet.
*Lien vers la documentation du SMF : ￼http://www.culture.gouv.fr/documentation/joconde/fr/partenaires/AIDEMUSEES/methode.htm#APTN￼*
### Contexte historique
* **Genèse** : choisissez un terme dans le thésuraus Genèse fourni par le Service des Musées de France.
* **Objets liés** : vous pouvez lier des objets à l’objet que vous décrivez
* **Historique** : champ texte vous permettant de décrire le contexte historique de l’objet
* **Lieu et précisions sur le lieu** : lien vers le fichier des lieux, sélectionnez un lieu et précisez s’il s’agit d’un lieu d’utilisation / destination , de création, de découverte ou de récolte
*Lien vers la documentation du SMF : ￼http://www.culture.gouv.fr/documentation/joconde/fr/partenaires/AIDEMUSEES/methode.htm#LIEU￼*
* **Géographie historique** : champ vous permettant de préciser le lieu
*Exemple* :\* Asie mineure, Ionie\*
*Lien vers la documentation du SMF : ￼http://www.culture.gouv.fr/documentation/joconde/fr/partenaires/AIDEMUSEES/methode.htm#GEOHI￼*
* **Utilisation, destination et précisions**  : choisissez un terme au sein du thesaurus « utilisation / destination » proposé par le SMF afin de préciser la fonction et l’usage de l’objet.
*Lien vers la documentation du SMF : ￼http://www.culture.gouv.fr/documentation/joconde/fr/partenaires/AIDEMUSEES/methode.htm#UTIL￼*
* **Méthode de découverte, collecte, ou de récolte d’un objet** : précisez la méthode utilisée lors de la découverte, de la collecte ou de la récolte d’un objet.
* **Date de découverte, collecte, récolte** : indiquez la date de la découverte, de la collecte ou de la récolte de l’objet.
*Lien vers la documentation du SMF : ￼http://www.culture.gouv.fr/documentation/joconde/fr/partenaires/AIDEMUSEES/methode.htm#DATEDECV￼*
* **Découvreur** : champ lié au fichier des entités, saisissez ici le nom du découvreur.
### Informations complémentaires
* **Exposition** : champ texte permettant de préciser les expositions dans lesquelles l’objet a été exposé ; les expositions actuelles sont décrites dans une fiche Exposition reliée à l’objet.
* **Bibliographie ou note de publication** : champ de texte enrichi dans lequel vous pouvez saisir une note du publication
* **Première date de présence** : indiquez ici la 1ère date de présence du bien dans les collection
* **Commentaires** : Saisissez ici toutes les informations que vous n’avez pu saisir ailleurs qu’il s’agisse des informations liées à la conservation de l’objet ou à son contexte d’acquisition.
*Lien vers la documentation du SMF : ￼http://www.culture.gouv.fr/documentation/joconde/fr/partenaires/AIDEMUSEES/methode.htm#COMM￼*
* **Date de vol ou de disparition** : date de vol éventuelle
* **Date à laquelle le bien a été retrouvé** : si vol, date à laquelle l’objet a été retrouvé
* \*\* Mention à porter en cas de radiation\*\* : mention que l’on souhaite inscrire au registre inventaire en cas de radiation.
* **Rédacteur** : rédacteur de la notice : relié au fichier des entités
### Conservation et régie
* **Constat d’état initial**  : décrivez le constat d’état initial de l’objet : date du constat, constat, état et commentaires ; vous pouvez associer à ce constat tout document numérique souhaité.
* **Lien vers fiche conservation / restauration** : lien vers la ou les fiches de conservation ou de restauration 
* **Emplacement** : sélectionnez l’emplacement de l’objet au sein du fichier emplacement.
* **Date d’arrivée à l’emplacement actuel** : date d’arrivée de l’objet à l’emplacement actuel.
### Représentations Média
Placez ici tous les médias représentant l’objet : photographies, images, vidéos, enregistrements sonores…
 Pour télécharger plusieurs représentations de votre enregistrement, cliquez sur « Ajouter une représentation ». Chaque représentation est un enregistrement à part entière
 *CollectiveAccess supporte de nombreux types de fichiers. Pour consulter la liste complète des types de fichiers, rendez-vous sur le wiki : ￼http://docs.collectiveaccess.org/wiki/Supported\_Media\_File\_Formats￼*.
* **Formats de fichier** : Pour information, les formats courants sont : JPEG, TIFF, MPEG-4, vidéo FLASH, FLV, WAV, AIFF, MP3, PDF
* **droits du média** : attribuez les droits d'accès aux fichiers média dans le menu déroulant. Ceux-ci sont configurables dans le menu listes & vocabulaire.
* **statut** : attribuez un statut de catalogage à votre média ; celui-ci peut être différent du statut attribué à l'objet.
* **accès**  : choisissez si ce média est accessible ou non au public sur Pawtucket, interface publique de CollectiveAccess ; ce niveau d’accès peut être différent de celui-ci attribué à l'objet.
* **définir par défaut **: en cliquant sur « définir par défaut », le média s'affichera en premier dans l'interface de catalogage et sur le catalogue en ligne, s'il y a plusieurs images de l'enregistrement.
- **télécharger le média** : cliquez sur ce bouton pour télécharger les médias.
### Accès
Choisissez ici l’accès de l’objet au public et détaillez les conditions.
### Relations
Sont rappelées dans cet écran toutes les relations entre l’objet et les différents enregistrements de CollectiveAccess saisies dans les précédents écrans : Collection, Entités, Objets,…
Depuis cet écran, vous pouvez également renseigner deux champs spécifiques pour le catalogage de votre objet :
- la géolocalisation ou **géoréférencement** : ce champ vous permet de faire correspondre un emplacement géographique à votre objet. Saisissez l'adresse désirée, CollectiveAccess vous retournera les coordonnées géographiques de l'adresse fournie, ainsi que son emplacement sur une carte aérienne. 
	Vous pouvez également créer la géolocalisation dans Google Earth, puis l'importer dans CollectiveAccess.
- le nom **géographique** :  À la place d'une adresse spécifique vous pouvez saisir dans ce champ un nom de lieu, comme un parc, un lac ou glacier... Saisissez les premiers caractères de ce nom, un menu déroulant vous présente les noms reconnus. Après sélection, vous récupérez les coordonnées géographiques et un affichage sur une carte aérienne.
### Résumé
Les informations saisies sont résumées dans cet écran.
Sélectionnez le format d’affichage dans le menu déroulant présent en faut à droite :
* le format d’affichage « Registre d’inventaire » affichera les 18 colonnes demandées par le Service des Musées de France lors de l’inscription d’un objet à l’inventaire. Les rubriques remplies apparaissent en gras, les autres sont grisées.
* vous retrouverez ici également tous les formats d’affichage que vous aurez créez (\*dans Gérer \> mes affichages, support « Gestion des affichages »)