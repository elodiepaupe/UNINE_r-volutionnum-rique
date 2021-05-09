---
marp: true
---

Université de Neuchâtel
Master en littératures

# TG: Histoire du livre et sa troisième révolution (numérique)
## Cours 9: introduction à LaTeX

Élodie Paupe 
chaire de philologie classique et d'histoire ancienne

3 mai 2021

---
### Objectifs du cours 

* créer un document de la classe "book" 
* différence avec la classe "article"
* structurer avec la classe "book"
* insérer une image

---

## Préambule et document 
Un document .tex est composé d'un préambule dans lequel on déclare les packages utilisés et du contenu à proprement parlé qui figure dans l'environnement principal borné par les commandes `begin{document}` et `end{document}`. 

Dans le document test, le préambule est le suivant: 
```latex
\documentclass[12pt,a4paper]{book}
\usepackage{fontspec}
\usepackage{xunicode}
\usepackage{polyglossia}
    \setmainlanguage{french}
```
--- 
```latex
\documentclass[12pt,a4paper]{book}
```

La déclaration du document permet de choisir quel type de document on va rédiger: book, article, letter, beamer, etc. Il va déclencher une série de choix de mise en page (types de niveaux de titres, marges, entêtes)

La classe de valeur `book` permet ainsi de générer automatiquement un fichier qui prendra la forme d'un livre avec une page de titre automatisé, la gestion des entêtes et des numéros de page, etc. 

Ici, la classe porte des options: la taille de police et de papier. On aurait pu ajouter des informations sur le nombre de colonnes, par exemple. 

--- 

```latex
\usepackage[<...>]{...}
```
Les éléments présentés selon cette syntaxe sont des packages. Chaque package fonctionne comme une extension ou un plug-in qui vient apporter des compétences complémentaires à votre document. 

---
```latex
\usepackage{fontspec}
\usepackage{xunicode}
\usepackage{polyglossia}
    \setmainlanguage{french}
```

* fontspec permet d'afficher correctement la typographie. 
* xunicode permet la prise en charge des des caractères unicodes (= utf-8)
* polyglossia permet de gérer les langues dans un document
* la commande `\setmainlanguage{french}`permet de définir la langue et donc les règles typographiques appliquées dans le document.

--- 
Compilons le document. 

--- 
```latex
\begin{document}
\title{L’ARRESTATION D’ARSÈNE LUPIN}
\author{Maurice Leblanc}

\maketitle

....
\end{document}
```
Ces lignes permettent de définir les informations qui seront automatiquement affichées dans la page de titre dont l'apparition est commandée par la commande `maketitle`. 

---
L'environnement `\begin{document}... \end{document}` contient le corps de texte. 
Par environement, on entend une portion de texte qui doit obéir à des règles spécifiques: 
il existe un environnement pour créer des listes (`begin{itemize}`), pour insérer une figure (`\begin{figure}`). 

---
## Rédiger le corps de texte

* Une ou plusieurs espace → une espace
* Pas d'espace devant :!? → une espace insécable
* Un retour à la ligne → une espace
* Une ligne vide → un changement de paragraphe
* Plusieurs lignes vides → un changement de paragraphe

--- 
Commenter un document: 
```latex
% Ce qui figure ensuite est un commentaire qui n'est pas interprété par l'ordinateur au moment de compiler le document.
```

---
### Objectifs du jour: 

* créer un document de la classe "book" 
* différence avec la classe "article"
* structurer avec la classe "book"
* insérer une image

---
### Classe "article"

Modifions la classe en article pour voir ce que cela change. 

--- 
Dans la classe article, on peut ajouter un résumé avec l'environnement `abstract`. Essayez d'en ajouter un. 

--- 

### Structuer avec la classe "book" 
Pour ajouter des titre, on utilise les commandes suivantes: 
```latex
\part 
\chapter
\section
\subsection
\subsubsection
\paragraph
\subparagraph
```
Essayez-les pour voir les changements. 

--- 
