# BUILD.md

```
brew install python3
pip3 install mkdocs
pip3 install mkdocs-material
pip3 install markdown-include
pip3 install mkdocs-minify-plugin
pip3 install mkdocs-git-revision-date-localized-plugin
pip3 install -e git+https://github.com/jwaschkau/mkpdfs-mkdocs-plugin.git#egg=mkpdfs-mkdocs
brew install weasyprint
# Problem with weasyprint and latest mac M1 homebrew python versions
sudo mkdir /usr/local/lib
local sudo ln -s /opt/homebrew/opt/glib/lib/libgobject-2.0.0.dylib /usr/local/lib/gobject-2.0
sudo ln -s /opt/homebrew/opt/pango/lib/libpango-1.0.dylib /usr/local/lib/pango-1.0
sudo ln -s /opt/homebrew/opt/harfbuzz/lib/libharfbuzz.dylib /usr/local/lib/harfbuzz
sudo ln -s /opt/homebrew/opt/fontconfig/lib/libfontconfig.1.dylib /usr/local/lib/fontconfig-1
````

## Patch

https://github.com/Kozea/WeasyPrint/issues/1426
The import has changed since v53. Now it’s from weasyprint.text.fonts import FontConfiguration.

```
code /Users/gautiermichelin/Library/Python/3.9/lib/python/site-packages/mkpdfs_mkdocs
```

Modifier :

- generator.py : ligne 9
- mkpdfs.py : ligne 12


https://github.com/comwes/mkpdfs-mkdocs-plugin/issues/14
AttributeError: module 'mkdocs.utils' has no attribute 'string_types'

## Running

```
mkdocs serve
```