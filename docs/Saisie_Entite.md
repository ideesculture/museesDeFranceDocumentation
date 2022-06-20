# 8. La saisie d’une entité dans CollectiveAccess

Dans CollectiveAccess, les entités (personnes physiques ou morales) sont gérées comme des autorités, c'est à dire des enregistrements autonomes qui sont ensuite liés à un ou plusieurs autres enregistrements : objets, entités, lieux, etc.. 
## Comment créer une entité ?
Pour créer une entité  :

- Depuis l’objet, lors de la saisie d’une personne liée, si celle-ci n’est pas déjà présente dans la base, CollectiveAccess vous propose de la créer au fil de l’eau. L’entité nouvellement créée alimente directement le fichier des entités.

Sinon :

- Cliquez sur le menu « Nouveau » dans la barre de navigation principale.
- Sélectionnez « Entité » dans le menu déroulant, puis choisissez un type (Famille, Personne physique, organisation etc...) pour créer un nouvel enregistrement.
*NB : la liste des types d'entités dépend de votre paramétrage. (cf. support de cours administration de CollectiveAccess)*

## Quelques conseils de saisie

Nous vous conseillons d’enregistrer vos modifications avant de passer à l'écran suivant, dans le cas contraire, une alerte vous demandera de confirmer que vous voulez quitter l’écran en cours sans enregistrer.

##### Enregistrer / Annuler / Supprimer
Pour enregistrer/annuler votre saisie ou supprimer votre objet, cliquez sur les boutons du même nom qui se trouvent en haut et en bas de votre écran de saisie.

##### Définir plusieurs valeurs 
Si vous avez besoin de définir plus d’une valeur pour un des champs affichés à l’écran, cliquez sur le + en bas du champ.

## Ecrans de saisie
Les écrans contiennent les champs d'informations nécessaires à la création d'une nouvelle entité.
*NB : les champs et écrans de saisie sont entièrement paramétrable (cf. support de cours administration de CollectiveAccess).*

### Informations de base (Informations basiques)
Cet écran contient les informations élémentaires pour démarrer un nouvel enregistrement.

#### Nom 
Saisissez un nom de famille (champ obligatoire), un prénom, éventuellement un préfixe et/ou un suffixe ; par défaut le sous-champ « nom pour l’affichage » sera constitué du prénom suivi du nom, si vous souhaitez le modifier, saisissez la valeur souhaitée dans la case.

#### Précisions sur l'entité
Indiquez ici les précisions que vous souhaitez apporter.

#### Identifiant de personne 
Il s’agit de l’identifiant de l’entité, celui-ci peut être généré automatiquement ; il sera rempli du numéro d’autorité en cas d’import.

#### Accès 
Sélectionnez dans le [menu déroulant](../types_de_champs/#1-liste-deroulante) si vous souhaitez que l’entité soit accessible au public ou non.

#### Statut 
Sélectionnez dans le [menu déroulant](../types_de_champs/#1-liste-deroulante) le statut de création de l'entité.

### Média
Ajoutez ici toute représentation média que vous jugerez utile à afficher/conserver en lien avec l’entité.

Cliquez sur "choisir un fichier" puis sélectionnez un document pour l'ajouter

### Contact
Cet écran vous permet de saisir les coordonnées de l’entité personne physique ou organisation.

#### Adresse
Saisissez les deux lignes d'adresse, la ville, le pays et le code postal de l'entité

#### Tél / Fax 
Saisissez le numéro de Téléphone de l'entité

#### Adresse Email 
Indiquez ici l'adresse e-mail de l'entité

#### Type d’adresse 
Choisissez le type d'adresse de l'entité 

### Information complémentaire
Vous pouvez donnez ici des compléments d’information sur l’entité :

#### Culture populaire  
Saisissez ici la civilisation à laquelle l'entité est associé

#### Groupe de gens 
Saisissez ici la communauté à laquelle l'entité est associé

#### Groupe linguistique :
La langue parlée par l'entité  

#### Note biographique sur les personnes 
Information concernant l'histoire de l'entité

#### Dates essentielles 
Indiquez ici la date de naissance et de mort de l'entité

#### Genre 
Précisez ici le genre de l'entité

#### Nationalité d'une personne 
Notez ici la nationalité de l'entité

#### Emploi d'une personne 
Saisissez l'emploi de l'entité

#### Salutation 
**???**

#### Son style / école 
Ce champ est lié au thesaurus « style / école » fourni par le Service des Musées de France

### Relations
Cet écran récapitule toutes les relations qui lient l’entité aux autres enregistrements de la base : objets, entités,lieux, occurrences, collections.

* lors de création d’un objet (par exemple), la sélection ou la saisie d’une entité ajoute directement l’objet en tant qu’objet lié de l’entité

* vous pouvez également saisir le lien entre une entité et un enregistrement directement depuis cet écran : dans le champ recherche, indiquez l’identifiant de l'enregistrement ou son nom :
	- la saisie d’au moins trois caractères dans la case de recherche vous propose une liste d’enregistrements contenant ces caractères,
	    - sélectionnez ensuite l’enregistrement souhaité.
	    - définissez le type de lien entre les deux enregistrements
	    - enregistrez : la nouvelle relation apparaît dans la fiche de l'entité et sera également affichée dans l’enregistrement (objet, entité…) lié.
		
La croix (x) située à droite d'une relation vous permet de la supprimer.

Si l’enregistrement recherché n’apparaît pas dans la liste déroulante, n’ayant pas encore été créé dans la base, CollectiveAccess vous donne la possibilité de le créer à la volée.

### Liens
Vous pouvez relier l'entité à un (ou plusieurs) site(s) web(s)

#### Nom du site web 
Donner le nom du site de l'entité

#### Url 
Donner le lien pour accéder au site de l'entité

### Résumé
L’écran Résumé récapitule les informations saisies dans la fiche entité, selon le format d’affichage sélectionné dans le menu déroulant présent en haut à droite de l’écran à coté de button 
vous permettant de télécharger le résumé de l'enregistrement en pdf.[^1]

[^1]:Vous pouvez créer de nouveaux formats d’affichages en allant dans le menu Gérer \> Mes affichages. (cf. Support administration de CollectiveAccess, gestion des formats d’affichages).
Si le menu et le bouton ne sont pas présents c'est qu'aucun n'affichage n'as été crée.

### Les logs
Les logs correspondent à l'historique de l’enregistrement.
Cet écran présente tous les changements apportés à l’enregistrement et indique l’identifiant de l’utilisateur ayant effectué ces modifications, la nouvelle valeur mise en place, ainsi que la date et l’heure correspondant à la modification.

[image-1]:	chapter6_images/creer-entite.png 
