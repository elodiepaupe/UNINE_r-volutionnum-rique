---
marp: true
---

Université de Neuchâtel
Master en littératures

# TG: Histoire du livre et sa troisième révolution (numérique)
## Cours 10: introduction à LaTeX (suite)

Élodie Paupe 
chaire de philologie classique et d'histoire ancienne

10 mai 2021

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

* créer un document de la classe "book" ✔︎
* différence avec la classe "article"
* structurer avec la classe "book"
* insérer une image

---
### Classe "article"

Modifions la classe en article pour voir ce que cela change. 

--- 
Dans la classe article, on peut ajouter un résumé avec l'environnement `abstract`. 
Essayez d'en ajouter un. 

---

[Exercice 1](exercices/ArseneLupin_exo1.tex)

--- 
Lorsqu'on compile un document LaTeX, on obtient un PDF et des fichiers de travail qui servent à réaliser la compilation: 
* .tex = le fichier texte

* .pdf = le fichier final après compilation
* .aux = les informations sur les références (les packages y inscrivent des informations, des données sur la bibliogrpahies, etc.)
* .log = le journal de compilation qui indique notamment les erreurs (très utile!)

---
Ces fichiers (il pourrait y en avoir d'autres, .toc par exemple) peuvent être supprimés. Ils permettent d'augmenter la vitesse de compilation. 

--- 
### Structurer avec la classe "book" 
Pour ajouter des titre, on utilise les commandes suivantes: 
```latex
\part{}
\chapter{}
\section{}
\subsection{}
\subsubsection{}
\paragraph{}
\subparagraph{}
```

---
Par défaut, les titres sont numérotés pour que la numérotation n'apparaisse pas, on utilise l'astérisque: 
`\chapter*`

Un titre non numéroté n'apparaît pas dans la table des matières, mais il est possible de contourner ce problème avec la commande 
```latex
\addcontentsline{toc}{chapter}{Introduction}
\chapter*{Introduction}
```

---
En plus de la titraille, LaTeX permet de structurer un document de classe `book` en quatre parties qui ont des réalisations numérales différentes: 
* `\frontmatter` va contenir le préambule d'un livre (avant-propos, sommaire, introduction) → titre non numérotés, mais présents dans la table des matières, numéros de pages en chiffre romains
* `\mainmatter` va contenir le travail → titres numérotés et numérotation des pages en chiffres arabes
* `\appendix` va contenir les appendices → chapitres renommés "appendices" et numérotés avec des lettres
* `\backmatter` va contenir les index, glossaires, table des matières, etc. → pas de numéro de chapitre, mais présent dans la table des matières
---

[Exercice 2](exercices/ArseneLupin_exo2.tex)
À créer.

---
### Environnements
L'environnement `\begin{document}... \end{document}` contient le corps de texte. 
>Par environement, on entend une portion de texte qui doit obéir à des règles spécifiques.

Les environnements se contiennent les uns les autres, mais ne peuvent pas se chevaucher, comme les balises HTML.

---
Il existe un environnement pour créer 
* des listes à puce (`begin{itemize}`)
* des listes numérotées (`begin{enumerate`})

→ Pour insérer chaque élément de la liste, on utilise la commande `\item`. 

* des listes de définition (`begin{description}`)

→ Pour insérer un élément de cette liste, on utilise la commande `\item[]` entre les parenthèses carées figurent le lemme à définir (un mot, une date, etc.)

---
On peut imbriquer les listes: 
```latex
\begin{itemize}
    \item Un élément de premier niveau 
    \begin{enumerate}
        \item Premier sous élément
        \item Second sous élément 
    \end{enumerate}
    \item Un autre élément de premier niveau 
\end{itemize}
```

---
Mais aussi 
* pour insérer une figure (`\begin{figure}`)
* pour gérer les changements de langues (par exemple: `begin{english}`) pour adapter la typographie et les césures de mots

---
On peut signaler un changement de langue annoncé dans le préambule
* en créant un environnement (cf. précédemment)
* en utilisant une commande `\textenglish{here the text}` 

---
Si vous utilisez la langue latine, les règles de césure et de typographie employées sont celles de la langue anglaise. 

Pour utiliser les règles francophones, il faut redéfinir l'environement `latin` dans le préambule, autrement dit programmer un nouveau fonctionnement pour cet environnement: 
```latex
\renewenvironment{latin}{\begin{hyphenrules}{latin}}
{\end{hyphenrules}}
```

--- 
Il existe un environnement qui permet de mettre en forme les citations longues: `\begin{quote}`. Pour l'utiliser, il faut appeler un package spécial, `\usepackage{csquotes}`.
```latex
... 
\usepackage{csquotes}

\begin{document}
   
   
\end{document}
```

---
## Commandes porteuses de sens
* `\emph{}` met en évidence un morceau de texte par un italique.
* `\footnote{}` insère une note de bas de page.
* `\endnote{}` insère une note de fin de document. 
* `\marginpar{}` insère une annotation marginale.

---
## Commandes porteuses de mise ne forme
* `\textit{}`
* `\textbf{}`
* `\textsuperscript{}`

--- 
## Mettre en forme la poésie 
Si on doit citer uniquement un extrait de pésie, on peut se contenter d'utiliser l'envionnement `verse`. 

1. Dans le document, on ouvre crée un environnement avec `begin{verse}`. 
1. Chaque vers se termine par `\\` sauf le dernier. 

---
```latex
\begin{document}
    \begin{verse}
    Je fais souvent ce rêve étrange et pénétrant \\
    D'une femme inconnue et que j'aime et qui m'aime \\
    Et qui n'est chaque fois ni tout à fait la même \\
    Ni tout à fait une autre et m'aime et me comprend
    \end{verse}
\end{document}
```

---
Pour mettre en forme de la poésie, il faut ajouter un package `verse` avec le même environnement. Ainsi, on peut gérer la numérotation automatique, l'indentation, etc.

1. Dans le préambule du document, on déclare le package `\usepackage{verse}`
1. On utilise la commande `\poemlines{4}` pour paramétrer la numérotation tous les quatre vers.
1. Chaque vers se termine par la macro `\\` sauf le dernier de chaque strophe `\\!` et le dernier du poème. 

--- 
```latex
... 
\usepackage{verse}

\begin{document}
    \begin{verse}
    \poemlines{4}
    Je fais souvent ce rêve étrange et pénétrant \\
    D'une femme inconnue et que j'aime et qui m'aime \\
    Et qui n'est chaque fois ni tout à fait la même \\
    Ni tout à fait une autre et m'aime et me comprend 
    \end{verse}
\end{document}
```

--- 
1. Si on souhaite un extrait et que la numérotation des vers ne commence pas à 1, on utilise la commande `\setverselinenums{}{}`
    * le premier argument est le numéro du vers
    * le deuxième argument est le vers à partir duquel il faut numéroter
1. `\poemtitle` permet de donner un titre au poème.

```latex
\begin{document}
    \begin{verse}
    \poemlines{2}
    \setverselinenums{2}{2}
    \poemtitle{Un rêve étrange}

    D'une femme inconnue et que j'aime et qui m'aime \\
    Et qui n'est chaque fois ni tout à fait la même \\
    Ni tout à fait une autre et m'aime et me comprend
    \end{verse}
\end{document}
```

--- 
Par défaut, le package `verse` ne dispose pas d'une commande pour faire figurer les informations liées à l'auteur, mais LaTeX permet de créer des commandes pour définir des mises en formes personnalisées. Le code permettant la création d'une nouvelle commande est placée dans le préambule.

```latex
\newcommand{\auteur}[1]{%
   \nopagebreak{\raggedleft\footnotesize #1\par}}
```
La commande ainsi créée est appelée avec la macro `\auteur{}`.

--- 

[Exercice 3](exercices/Musset_exo3.tex)

--- 
Les packages disposent tous d'une documentation qui décrit leurs possibilités et les commandes disponibles. 

Ces informations et les coordonnées des concepteurs sont notamment disponibles sur [https://www.ctan.org](https://www.ctan.org).

Pour le package [verse](https://www.ctan.org/pkg/verse).

---
Certains caractères sont employés par LaTeX dans les commandes `%_&$#^`
et ne peuvent donc pas être utilisés directement: on dit qu'on doit les échapper en les 
faisant précéder de `\`: 
* pour écrire "Les rouges & verts" en écrira en LaTeX `les rouges \& verts`
* le slash s'insère avec `\textbackslash`
* le ~ s'insère avec `\textasciitilde`
* le ^ s'insère avec `\textasciicircum`


--- 
## Mettre en forme une édition bilingue

Pour réaliser une édition bilingue, on va utiliser les packages reledpar et reledmac que l'on déclare dans le préambule.

Ces packages permettent de réaliser des éditions bilingues en deux colonnes parallèles ou sur deux pages. Les notes de bas de page appelées sont placées sous la page concernées. Pour mettre le texte en parallèle, on utilise l'encodage suivant.

---
```latex
\begin{pairs}
    \begin{Leftside} 
    \beginnumbering
    \pstart
        Le texte d'un paragraphe dans une langue (généralement la langue source).  
    \pend
    \pstart
        Un autre paragraphe
    \pend
    \endnumbering
    \end{Leftside}

    \begin{Rightside} 
    \beginnumbering
    \pstart
        Le premier paragraphe de la traduction. 
    \pend
    \pstart
        Le second.
    \pend
    \endnumbering
    \end{Rightside}
\end{pairs}
\Columns

```

---
```latex
\begin{pages}
    \begin{Leftside} 
    \beginnumbering
    \pstart
        Le texte d'un paragraphe dans une langue (généralement la langue source).  
    \pend
    \pstart
        Un autre paragraphe
    \pend
    \endnumbering
    \end{Leftside}

    \begin{Rightside} 
    \beginnumbering
    \pstart
        Le premier paragraphe de la traduction. 
    \pend
    \pstart
        Le second.
    \pend
    \endnumbering
    \end{Rightside}
\end{pages}
\Pages

```

---

[Exercice 4](exercices/Utopie_exo4.tex)

--- 
Pour ajouter des notes critiques sur le texte source (par exemple un apparat critique), on utilise la commande suivante: 

```latex
\edtext{ici le mot du texte qui connaît des variantes}{\Afootnote{Ici la variante que vous souhaitez nommée }}
```

Il est possible d'avoir jusqu'à 5 "étages" de note avec les commandes: 
* `\Afootnote{}`
* `\Bfootnote{}`
* `\Cfootnote{}`
* `\Dfootnote{}`
* `\Efootnote{}`

--- 
Par défaut, les notes vont se mettre à la ligne les unes des autres, mais dans le cas d'un apparat critique, on perd énormément de place. On va donc demander au package de placer les notes à la suite les unes des autres sur une seule ligne. Pour cela, on modifie le fonctionnement général du package dans le préambule: 
```latex
\usepackage{reledmac}
    \Xarrangement{paragraph}
```

--- 
La même syntaxe est possible avec `\Aendnote{}` qui produit des notes de fin de document. Par défaut, celles-ci ne s'impriment pas, il faut appeler leur impression avec la commande `\doendnotes` à l'endroit où on souhaite les voir. 

--- 

[Exemple](exercices/Utopie_exo6_corr.tex)

---



