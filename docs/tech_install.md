# 2. Installation

## Publication sur GitHub Pages

La documentation est publiée depuis la branche `gh-pages` et servie à l'adresse [documentation.ideesculture.com/museesDeFranceDocumentation](https://documentation.ideesculture.com/museesDeFranceDocumentation/).

```
git pull
mkdocs gh-deploy --remote-branch gh-pages
```

Récupérez toujours les derniers commits avant de déployer : `gh-deploy` publie le contenu du dépôt local et écraserait des modifications poussées depuis un autre poste.

Le dossier `site/` est versionné : régénérez-le (`mkdocs build`) et commitez-le avec les sources.

## Installation des outils de développement de la documentation

Le site est généré avec MkDocs 1.6 et le thème Material for MkDocs 9 (versions en service en septembre 2026 : MkDocs 1.6.1, Material 9.7.6).

- Installer Homebrew

```
brew install python3
pip3 install "mkdocs<2" mkdocs-material
```

Restez sur MkDocs 1.x : MkDocs 2.0 supprime le système de plugins et casse les personnalisations du thème (dossier `overrides/`). La contrainte est aussi fixée dans `requirements.txt`.

Commandes utiles :

```
mkdocs serve   # prévisualisation locale avec rechargement automatique
mkdocs build   # génération du site dans le dossier site/
```

## Génération PDF (mkPdfs)

Le plugin mkPdfs n'est plus activé dans `mkdocs.yml`. Les instructions ci-dessous ne servent que si vous le réactivez.

Installer les prérequis :

```
brew install cairo pango gdk-pixbuf libffi
brew install libmagic
pip3 install WeasyPrint mkpdfs-mkdocs
```

Pour personnaliser la feuille de style, installer les dépendances :

```
cd mkpdfs-design
npm install
```

Puis mettre à jour la CSS depuis les fichiers SCSS :

```
npm run build
```
