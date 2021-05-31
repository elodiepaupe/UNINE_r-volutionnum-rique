---
marp: true
---

Université de Neuchâtel
Master en littératures

# TG: Histoire du livre et sa troisième révolution (numérique)
## Cours 12: introduction à LaTeX (suite) et conclusion

Élodie Paupe 
chaire de philologie classique et d'histoire ancienne

31 mai 2021

---

## Insérer des images
Pour insérer des images dans un fichier `.tex`, on va 
* appeler le package `graphicx`; 
* faire appel à l'environnement `figure`; 
* utiliser le chemin relatif ou absolu qui permet d'indiquer à l'ordinateur où se trouve le fichier en question sur l'ordinateur dans la commande `\includegraphics` comprise dans l'environnement `figure`; 
* utiliser la commande `\caption` pour introduire une légende

--- 
```latex
\begin{figure}
	\includegraphics[scale=0.2]{tablette_argile.jpg}
	\centering
	\caption{Tablette proto-élamite provenant de l’Acropole de Suse, 
    avec empreinte de sceau-cylindre au verso, 4200-2800 avant J.-C., Suse, argile. 
    (\href{https://www.louvre.fr/oeuvre-notices/tablette-protoelamite-avec-empreinte-de-sceau}
    {Musée du Louvre, Sb 2801})}	
\end{figure}
```
--- 
On peut également spécifier moins d'informations et utiliser directement 
```latex
\includegraphics[scale=0.2]{tablette_argile.jpg}
```


---
# Réaliser une présentation:
# utiliser la classe `beamer`

---

## Préambule
Pour réaliser une présentation avec LaTeX, on utilise la classe de documents `beamer`.

* Déclaration des packages dans le préambule (attention, certains d'entre eux ne sont pas construits pour être employés dans une présentation)
* modification des options
* remplissage des métadonnées

---
```latex
\documentclass[french,10pt,handout]{beamer} 
	%handout permet d'afficher la présentation sans les effets
	\setbeameroption{hide notes} % Only slides
	%\setbeameroption{show notes} % les deux
	%\setbeameroption{show only notes} % Only notes
	
\usepackage{xunicode}
\usepackage{polyglossia}
	\setmainlanguage[variant=swiss,frenchpart=false]{french}

\title[Cours 1]{TG: L'histoire du livre et sa troisième révolution (numérique)\\
    cours 12: dernier atelier}
\author{Élodie Paupe}
\institute{Master en littérature\\ semestre de printemps -- Université de Neuchâtel}
\date{\today}
\logo{\includegraphics[height=1cm]{UNINE_gris_pos.jpg}}

```

--- 
## Contenu et environnement `frame`
Le contenu de la présentation est compris dans l'environnement `document` et chaque diapositive dans un environnement `frame`

```latex
\begin{document}

\begin{frame}
    \maketitle
\end{frame}

\begin{frame}
    \frametitle{Voici le titre de ma diapositive}
    Ici, la première diapositive après celle de titre
\end{frame}

\end{document}

```

---

L'environnement `frame` peut également être encodé

```latex
\frame{
    \maketitle
}
```

---
Dans une diapositive, on peut faire apparaître des paragraphes de texte ou des listes. 

---
Paragraphes: 

```latex
\begin{frame}
    Voilà un paragraphe

    Puis un deuxième

    Puis un troisième 
\end{frame}

```
---
Liste: 

```latex
\begin{frame}
    \begin{enumerate}
        \item Premier élément
        \item Deuxième élément
        \item Troisième élément
    \end{enumerate}
\end{frame}
```
---

## Animer l'apparition du contenu
Pour faire apparaître les paragraphes les uns après les autres, on utilise la commande `\pause`

```latex
\begin{frame}
    Ici un premier paragraphe
    \pause
    
    Puis un deuxième
    \pause 
    
    Puis un troisième
    \pause

    Puis du texte et de l'image.
    \includegraphics[height=1cm]{UNINE_gris_pos.jpg}    
    
\end{frame}
```
--- 
Il existe d'autres commandes qui permettent d'appeler les zones par couche sans que celles-ci soient forcément dans l'ordre: 

```latex
\begin{frame}
    \onslide<2>
    Ici un premier paragraphe
    
    \onslide<1->
    Puis un deuxième
    
    \onslide<3->
    Puis un troisième
	
    \onslide<4>
    Puis du texte et de l'image.
    \includegraphics[height=1cm]{UNINE_gris_pos.jpg}    
    
\end{frame}
```

--- 
* `\onslide` permet de définir à quel moment l'élémet qui suit va apparaître 
    * `<1>` = seulement dans la première couche
    * `<1->` = dès la première couche et jusqu'à la fin
    * `<1-2>` = seulement dans les deux premières chouches
    * `<-3>` = depuis le début jusqu'à la couche 3

Il existe d'autres commandes (`\only{}, \textbf{}, \color{}, \alert{}`) qui permettent de régler l'apparition.

---
Dans une liste (à puce ou autre), on utilise également le même procédé dans une liste: 

```latex
\begin{frame}
    \begin{itemize}
        \item<1-> Premier élément
        \item<2> Deuxième élément
        \item<3> Troisième élément
    \end{itemize}
\end{frame}
```

---
Pour faire apparaître les points dans l'ordre, on peut spécifier la chose une seule fois la chose sur l'environnement `itemize` (ou `enumerate`): 

```latex
\begin{frame}
    \begin{itemize}[<+->]
        \item Premier élément
        \item Deuxième élément
        \item Troisième élément
    \end{itemize}
\end{frame}
```

--- 
## Modèles et design
Le design des présentations réalisées avec `beamer` ne sont pas leur point fort, mais on les reconnaît immédiatement. 

Pour modifier le modèle par défaut, on fait appel à un package: 

```latex
\usepackage{beamerthemesplit}
    \usetheme{Singapore}
    \usecolortheme{seahorse}
```

On dispose de deux options pour modifier la disposition (`\usetheme{}`) identifiée par un nom de ville ou la gamme de couleurs (`\usecolortheme{}`) identifiée par un animal (on a l'humour qu'on mérite).

[Aperçu des possibilités](https://hartwork.org/beamer-theme-matrix/)

---
### Afficher le plan de la séance
Pour afficher le plan de la séance, il faut ajouter des `\section` et des `\subsection` (ou pas). 

Les `\section` se placent entre deux environnements `frame`, autrement dit on ne met pas le titre d'une partie dans une diapositive. 

Ces sections sont reprises dans la plupart des thèmes pour afficher la progression de la présentation.

---
```latex
\section{Introduction}
    \frame{Ici une première slide}

    \frame{Ici une seconde}

\section{Première partie}

    \frame{}

\section{Deuxième partie}

    \frame{}

\section{Conclusion}

    \frame{}
```

--- 
Pour faire apparaître le plan, on doit placer le code suivant dans le préambule: 
```latex
    \AtBeginSection[] %pour faire apparaître le plan au début de chaque section
    {
      \begin{frame}
      \frametitle{Plan de la séance}
      \tableofcontents[currentsection, hideothersubsections]
      \end{frame} 
    }
```

---

Pour les sous-sections: 

```latex
    
    \AtBeginSubsection[] %pour faire apparaître le plan au début de chaque sous-section
    {
      \begin{frame}
      \frametitle{Plan de la séance}
      \tableofcontents[currentsection, currentsubsection]
      \end{frame} 
    }
```

---
On peut ajouter des notes qui ne font pas partie de la présentation dans un document `beamer` en utilisant la commande `\note{}` en dehors d'un environnement `frame`. 

```latex
\frame{
    Ici une information importante.
}
\note{
    Ici, l'information importante que je devrai dire. 
}
```
---
On règle la compilation ou non des notes dans le préambule: 

```latex
	\setbeameroption{hide notes} % Only slides
	%\setbeameroption{show notes} % les deux
	%\setbeameroption{show only notes} % Only notes
```

---
[Présentation d'overleaf](overleaf.md)

[Exercice](exercices/exercice1.md)