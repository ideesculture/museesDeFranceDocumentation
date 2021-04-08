# 2. Installation

Cette documentation a été générée avec MkDocs sur Mac OS.

La version HTML a été généré via MkDocs puis publiée sur github pages.

La version PDF est générée avec le plugin MkPDFs for MkDocs, qui utilise WeasyPrint.

## Publication sur Github Pages

```mkdocs gh-deploy```

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
