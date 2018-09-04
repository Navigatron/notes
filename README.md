# navigatron.github.io

These are My Notes.

files:
```
_includes/ - for mathjax magic
_layouts/ - to override the terrible two column layout
assets/ - to make the remaining column full width
content/ - where my actual content is
_config.yml - pull in the theme I'm using.
```

Inside `content`, there is a folder for each class.

Each class folder has (probably) two things:
```
index.md - to keep track of the notes
notes/ - a folder to hold each class's notes.
```

Notes taken each class are named like `AUG30.md`.

If I want the magic of MathJax, make this the first thing in a file:
```
---
mathjax: true
---
```

After the MathJax enabling, this should be first:
```
[up](../index.md)
```

linking upwards enables at least some form of user navigation.
