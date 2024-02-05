# 2. Installation

## Publication sur Github Pages

```mkdocs gh-deploy --remote-branch gh-pages```

## Installation des outils de développement de la documentation

- Installer Homebrew

```
brew install python3
brew install cairo pango gdk-pixbuf libffi
brew install libmagic
pip3 install WeasyPrint
pip3 install mkdocs==1.0.4 mkdocs-material==4.6.3 mkpdfs-mkdocs
```

## Personnaliser la feuille de style mkPdfs

Installer les prerequis

```
cd mkpdfs-design 
npm install
```

Pour mettre à jour la CSS depuis les fichiers SCSS

```
npm run build
```