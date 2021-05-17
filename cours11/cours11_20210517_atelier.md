---
marp: true
---

Université de Neuchâtel
Master en littératures

# TG: Histoire du livre et sa troisième révolution (numérique)
## Cours 11: introduction à LaTeX (suite)

Élodie Paupe 
chaire de philologie classique et d'histoire ancienne

17 mai 2021

---

[Exercice 1](exercices/exercice1.md)

---
## Créer des commandes
Pour automatiser des mises en page, on peut créer des commandes qui combinent sémantisme et mise en forme. Ces nouvelles commandes sont placées dans le préambule.

Pour ce faire, on utilise une syntaxe particulière: 
```latex
\newcommand\nomdelanouvellecommande{comportement}
```

---
Prenons par exemple l'introduction du texte de Jane Austen à partir de [Wikipedia](https://fr.wikipedia.org/wiki/Orgueil_et_Préjugés). On voudra peut-être mettre les titres en italique et automatiser la façon de marquer les siècles: 

```txt
Orgueil et Préjugés (Pride and Prejudice) est un roman de la femme de lettres anglaise Jane Austen paru en 1813. Il est considéré comme l'une de ses œuvres les plus significatives et est aussi la plus connue du grand public.
Rédigé entre 1796 et 1797, le texte, alors dans sa première version (First Impressions), figurait au nombre des grands favoris des lectures en famille que l'on faisait le soir à la veillée dans la famille Austen. Révisé en 1811, il est finalement édité deux ans plus tard, en janvier 1813. Son succès en librairie est immédiat, mais bien que la première édition en soit rapidement épuisée, Jane Austen n'en tire aucune notoriété : le roman est en effet publié sans mention de son nom (« par l'auteur de Sense and Sensibility ») car sa condition de « femme de la bonne société » lui interdit de revendiquer le statut d'écrivain à part entière.
Drôle et romanesque, le chef-d'œuvre de Jane Austen continue à jouir d'une popularité considérable, par ses personnages bien campés, son intrigue soigneusement construite et prenante, ses rebondissements nombreux, et son humour plein d'imprévu. Derrière les aventures sentimentales des cinq filles Bennet, Jane Austen dépeint fidèlement les rigidités de la société anglaise au tournant des xviiie et xixe siècles. À travers le comportement et les réflexions d'Elizabeth Bennet, son personnage principal, elle soulève les problèmes auxquels sont confrontées les femmes de la petite gentry campagnarde pour s'assurer sécurité économique et statut social. À cette époque et dans ce milieu, la solution passe en effet presque obligatoirement par le mariage : cela explique que les deux thèmes majeurs d'Orgueil et Préjugés soient l'argent et le mariage, lesquels servent de base au développement des thèmes secondaires.
Grand classique de la littérature anglaise, Orgueil et Préjugés est à l'origine du plus grand nombre d'adaptations fondées sur une œuvre austenienne, tant au cinéma qu'à la télévision. Depuis Orgueil et Préjugés de Robert Z. Leonard en 1940, il a inspiré quantité d'œuvres ultérieures : des romans, des films, et même une bande dessinée parue chez Marvel.
Dans son essai de 1954, Ten Novels and Their Authors, Somerset Maugham le cite en seconde position parmi les dix romans qu'il considére comme les plus grands. En 2013, Le Nouvel Observateur, dans un hors-série consacré à la littérature des xixe et xxe siècle, le cite parmi les seize titres retenus pour le xixe siècle, le considérant comme « peut-être le premier chef-d'œuvre de la littérature au féminin ».
```

---

On va créer une commande pour mettre le texte en italique: 
```latex
\newcommand\titre[1]{\textit{#1}}
```

* L'option permet de définir le nombre d'argument que prendra la commande `\titre`, ici un.
* L'argument de la nouvelle commande `{\textit{#1}}` précise que le contenu entre acolades de la commande créée `\titre{}` sera mis en italique. Pour préciser où ce contenu va figurer, on l'appelle avec `#1`.

---
On va créer une commande pour que les siècles en chiffre romains soient en petites manuscules et l'ordinal en exposant: 
```latex
\newcommand\siecle[2]{\textsc{#1}\textsuperscript{#2}}
```

* L'option précise que la commande aura deux arguments: `\siecle{}{}`
* Le premier argument (`#1`) sera en petits majuscules; le second (`#2`) sera en exposant. 

--- 
Pour tester, complétez le document [ci-joint](data/commande.tex)

---
## Mettre en forme le théâtre

---
Pour automatiser la mise en forme du théâtre, on va utiliser le package `thalie`. 

Lien vers la [documentation](https://www.ctan.org/pkg/thalie).

Il permet: 
* de gérer les tours de parole et les didascalies; 
* de gérer les mentions des autres personnages; 
* de gérer la liste des rôles; 
* de gérer les actes et les scènes, etc. 

---
Le principe est le suivant: les personnages sont déclarés dans un environnement `dramatis` va ensuite générer des commandes individuelles. Lorsque ce personnage est cité dans le texte, c'est sa commande qui est appelée, ce qui permet d'ajuster la façon dont le nom va être imprimé. 

---
### Liste des personnages 
```latex
\begin{dramatis} %[hidden]
	\character[cmd={philo}, drama={Philonique}, desc={avocat des poules}]{Philonique}
\end{dramatis}
```

L'environnement `dramatis` peut porter l'option `[hidden]` si on ne souhaite pas imprimer la liste des personnages.

--- 
```latex
\begin{dramatis} %[hidden]
	\character[cmd={philo}, drama={Philonique}, desc={avocat des poules}]{Philonique}
\end{dramatis}
```

Chaque personnage est présenté dans l'environnement dramatis avec la commande `\character`. Dans l'option, on trouve les valeurs suivantes
* `cmd={}`: permet de créer la commande du personnage
* `drama={}`: permet de définir le nom à imprimer dans la liste des personanges
* `desc={}`: permet de définir le personnage. Cette description va s'imprimer dans la liste des personnages. 

--- 
```latex
\begin{dramatis} %[hidden]
	\character[cmd={philo}, drama={Philonique}, desc={avocat des poules}]{Philonique}
\end{dramatis}
```

L'argument `{Philonique}` est le nom qui va s'imprimer dans le texte de la pièce.

--- 
[Exercice 2](exercices/exercies2.md)

--- 
Les paragraphes de didascalies peuvent être encodés avec l'environnement `dida`: 

```latex
\begin{dida}
La scène est à Séville, dans la rue et sous les fenêtres de Rosine, au premier acte ; et le reste de la pièce dans la maison du docteur Bartholo.
\end{dida}
```

--- 
### Actes et scènes

On marque le début d'un acte avec la commande `\act{}` et le début d'une scène avec `\scene{}`. Il est possible de ne pas y adjointe de contenu, mais dans ce cas, il faut laisser les acolades tout de même.

--- 
### Didascalies
* Pour faire apparaître un bloc de didascalie aligné à gauche, on utilise l'environnement `dida`. 
* Pour faire apparaître une didascalie dans le fil d'une réplique, on utilise la commande `\did{}`. 
* Pour faire apparaître une didascalie centrée (par exemple les personnage présents sur scène), on utilise la commande `\onstage`. 

---
### Tour de parole 
Lorsqu'un personnage prend la parole, on fait précéder le texte de la réplique de la commande du personange: 

```latex
\comte[seul, en grand manteau brun et chapeau rabattu. Il tire sa montre en se promenant.]
    Le jour est moins avancé que je ne croyais. 
    L’heure à laquelle elle a coutume de se montrer derrière sa jalousie est encore éloignée. 
    N’importe ; il vaut mieux arriver trop tôt que de manquer l’instant de la voir. 
    Si quelque aimable de la cour pouvait me deviner à cent lieues de Madrid, 
    arrêté tous les matins sous les fenêtres d’une femme à qui je n’ai jamais parlé, il me prendrait pour un Espagnol du temps d’Isabelle. 
    — Pourquoi non ? Chacun court après le bonheur. 
    Il est pour moi dans le cœur de Rosine. 
    — Mais quoi ! suivre une femme à Séville, quand Madrid et la cour offrent de toutes parts des plaisirs si faciles ? 
    — Et c’est cela même que je fuis ! Je suis las des conquêtes que l’intérêt, la convenance ou la vanité nous présentent sans cesse. 
    Il est si doux d’être aimé pour soi-même ! et si je pouvais m’assurer sous ce déguisement… Au diable l’importun !

```

--- 
La didascalie qui suit le nom du personnage peut être présentée en option. 

--- 
Dans la réplique du comte sont mentionnés des personnages de la pièce. On peut les identifier en ajoutant `name` à leur commande. 

```latex
Chacun court après le bonheur. Il est pour moi dans le cœur de \rosinename.
```

---

[Exercice 3](exercices/exercice3.md)
