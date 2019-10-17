# DocFX TOC Generator

## What is this?
This script is used to generate `toc.yml` file for every folder in documentation project.

## Prerequesties

First you should install `powershell-yaml`

```powershell
Install-Module powershell-yaml
```

## Installing Module
```powershell
Install-Module -Name docfx-toc-generator	
```

## FAQ

### How to use this module?

Install the module, then run `Build-TocHereRecursive` function in the root of the docfx project, besides `docfx.json`

### What is the limitation?

This module doesn't generate the root TOC (root of folder besides `docfx.json`), you should create that file yourself.

### What if I want to ignore a folder?

Simply create an empty `.nodoc` file in the root of the folder.

### How to give markdown files name, href, items and order?

The `href` and `items` property of item in `yaml` file is created automatically.
For naming and order use Front Matter style `yaml` meta data in markdown file:

```
---
name: Sample Page
order: 100 # higher has more priority
---

# Sample Page
```

### How to create hierarchy?

This module puts every non-index file(non-`index.md`) in the toc, then it includes every `index.md` files in subfolder in the toc, and other files in subfolders in the `items` subchild of `index` file. For example if you have such hierarchy:

```
|-- root-doc.md
|-- some-other-root-doc.md
>-- MyTopic
  |---- somefile.md
  |---- index.md
|
>-- OtherTopic
  |-- index.md
  |-- hello.md
```

This toc will be generated:

```yml
- name: Root Doc
  href: root-doc.md
- name: Some Other Root Doc
  href: some-other-root-doc.md
- name: My Topic
  href: MyTopic/index.md
  items:
    - name: Some File
      href: MyTopic/somefile.md
- name: Other Topic
  href: OtherTopic/index.md
  items:
    - name: Hello World!
      href: OtherTopic/hello.md
```

