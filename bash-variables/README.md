# La gestion des Variables

Lorsque l'on veut réaliser des scripts bash, il est essentiel de savoir utiliser à la fois les **variables** mais aussi les **extensions du shell**. Via l'utilisation de ces deux notions, il nous est possible de réaliser des lignes de commande, et donc des scripts, plus permissifs et réutilisables. 

Un paramètre est une entité qui va stocker des valeurs, ce qui correspond:
- Aux variables
- Aux arguments positionnels
- Aux paramètres particuliers

Une variable n'est de son côté ni plus ni moins qu'une sorte de boite portant un nom et possédant un contenu. Lorsque l'on assigne une valeur à une variable, on entre des données dans la boite, et lorsque l'on référence la variable, on cherche à ressortir le contenu de la boite pour nous en servir.

Pour créer une variable, il n'y a rien de plus simple. On commence par donner un nom à la variable puis on lui affecte une valeur avec le signe `=`:

```bash
nom_variable="Valeur de la variable"
```

Ce genre de variable s'appelle une variable **définie par l'utilisateur** car elle se trouve être définie dans le script. A contrario, il existe des variables de shell, qui se trouvent être des variables **définies par le shell**. Il est courant de nommer nos variables en lowercase de sorte à les différencier des variables shells, lesquelles sont écrites en uppercase.

Pour pouvoir par la suite nous servir de nos variables, il est possible d'utiliser une syntaxe de la sorte: 

```bash
echo "Hello ${nom_variable}"
```

> L'utilisation de variables est essentielle lorsque l'on veut faire du scripting, de sorte à nous éviter d'avoir à écrire en dur à chaque fois le mail d'une compagnie, ou le nom d'un fichier. En le stockant dans une variable et en référençant cette variable, on peut de la sorte se passer de devoir renommer plein d'emplacement de notre script en cas de changement de valeurs pour le mail et / ou le nom de fichier. On a juste à changer le contenu de la variable, et le tour est joué !

### Les variables du Shell

Les variables d'environnement sont des variables qui sont communes dans toutes les commandes et dans tout le contexte de notre shell. Par exemple, les variables les plus couramment utilisées sont les variables `PATH`, `HOME`, `USER`, `HOSTNAME`, `HOSTTYPE`, `PS1`.

Il existe deux types de variables de shell:
- Les variables du Bourne Shell, plus anciennes, au nombre de **10**
- Les variables du Bash Shell, plus récentes, au nombre de **95**
  - La variable `PATH` est une variable **Bash** permet de définir pour le shell quels sont les emplacements à rechercher dans le cas où l'on tape un nom de commande dans le shell. 
  - La variable `HOME` est utilisée pour stocker le chemin absolu vers le dossier personnel de l'utilisateur.
  - La variable `USER` contient de son côté le nom de l'utilisateur en cours d'utilisation du shell.
  - La variables `HOSTNAME` contient des informations concernant l'ordinateur en cours d'utilisation par l'utilisation (son nom). 
  - La variable `HOSTTYPE` de son côté offre des informations sur l'architecture interne de l'ordinateur, par exemple son processeur. Via cette variable, il est possible d'optimiser les scripts pour tel ou tel type d'architecture.
  - `PS1` est la variable qui sert à définir la syntaxe du prompt de notre terminal. Si l'on la change, alors il nous est possible de changer le texte affiché dans notre terminal.

### Les extensions de paramètres

Il est parfois nécessaire de manipuler les paramètres avant de les traiter. Pour cela, il va nous falloir étendre un peu notre syntaxe d'appel des paramètres de type variable: 

Pour transformer en lowercase ou uppercase une variable, on dispose de cette syntaxe:
```bash
ma_variable="DuPoDeD"

echo "Ma variable avec son premier caractère en lowercase: ${ma_variable,}"
echo "Ma variable avec son premier caractère en uppercase: ${ma_variable^}"

echo "Ma variable en lowercase: ${ma_variable,,}"
echo "Ma variable en uppercase: ${ma_variable^^}"
```

Pour connaitre la longueur du texte d'une variable: 

```bash
echo "Ma variable est de longueur: ${#ma_variable}"
```

Et pour créer des tranches d'une variable, la syntaxe est la suivante. Il est ici intéressant de savoir que l'indice commence à **0** et que l'on peut compter en valeur négative via un index négatif de **-1** ou plus (attention à ne pas ommettre l'espace dans ce cas de figure): 

```bash
echo "${variable_name:offset:length}"

echo "Les trois premier caractères de ma variable: ${ma_variable:0:3}"
echo "Ma variable à partir du troisième caractère: ${ma_variable:3}"
echo "A partir du caractère final N-3, les deux caractères suivant dans ma variable: ${ma_variable: -3:2}"
```

### La substitution des commandes

De façon similaire à lorsque l'on utilisait des noms de variables dans la syntaxe précédente, il est possible de placer des commandes du shell entre des parenthèses dans le but d'injecter leur résultat dans le contexte de notre chaine de caractères.

```bash
#! /bin/bash

current_time=$(date +%H:%m:%S)

echo "Hello $USER, it's actually $current_time!"
```

### Les opérations arithmétiques

Si l'on le veut, il nous est possible de nous servir de l'extension de shell permettant la manipulation d'équation dans le cadre de nos script. De la sorte, il devient possible de procéder à la transformation de variables avant leur affichage. Pour procéder à l'utilisation de cet extension du shell, la syntaxe est la suivante: 

```bash
echo $((expression))
```

On peut ainsi réaliser l'affichage de résultat de calculs simples:

```bash
echo $((4 + 2))
```

Mais cela devient tout de suite plus intéressant lorsque l'on décider de cumuler la chose avec des variables: 

```bash
x=4
y=2

echo $(($x + $y))

echo $((x + y))
```

Il est intéressant de noter que cette extension du Shell n'est pas capable de gérer les nombres à virgule, et une division du type `5 / 2` aura pour résultat `2`. De part cette limitation, il nous faudra souvent utiliser la commande `bc` dans le cadre d'opérations mathématiques. 

L'utilisation de cette commande est assez simple, lorsque l'on entre la commande dans notre shell, nous atteignons le programme de calculation. Pour en sortir, il nous faut entrer `quit`. Entre temps, chaque ligne de calcul que nous entrons se verra être récupérée et son résultat affiché en dessous. Il est tout à fait possible d'envoyer à la commande **bc** l'entrée standard via le **piping**:

```bash
echo "5/2" | bc # 2
```

 Si l'on veut avoir un résultat comportant des virgules, il nous faut utiliser `scale`, ce qui va altérer légèrement notre syntaxe précédente: 

```bash
echo "scale=2; 5/2" | bc # 2.50
```

### L'extension Tilde

Lorsque l'on veut travailler dans les dossier utilisateur, il est courant d'avoir recourt à l'utilisation de l'extension Tilde. Par utilisation de `~`, il est possible d'avoir directement la valeur de `/home/user`. De même, si l'on veut le dossier utilisateur d'une personne en particulier, on peut utiliser la syntaxe `~username` pour obtenir `/home/username`. Si l'on demande celui du super utilisateur, on va se voir présenter le dossier **/root** à la place. 

La valeur du dossier courant est stockée dans une variable d'environnement portant le nom de `PWD`, qu'il nous est possible d'utiliser dans le cadre de nos scripts. A côté de cela, il existe aussi une variable `OLDPWD` qui permet de garder en trace l'ancien emplacement du dossier courant utilisé par le terminal dans le cas d'un déplacement parmi la structure des dossiers de l'ordinateur. 

Dans le cadre de l'utilisation de l'extension Tilde, il est intéressant de savoir que les valeurs stockées dans **PWD** et dans **OLDPWD** sont accessible via respectivement `~+` pour **PWD** et `~-` pour **OLDPWD**.

### L'extension Brace

Si l'on souhaitee travailler avec une série de fichiers / dossier qui respectent une certaine structure, il est possible de nous servir de l'extension **Brace** qui se base sur l'utilisation des accolades. Il est possible de s'en servir de deux façon principale: 
- Dans le cadre d'un listing, où chaque valeur va être séparée de la précédente par une virgule `{a,b,c,d,e}`
- Dans le cadre d'une portée, où l'on spécifiera le début et la fin de la portée, le tout séparé par un tiret `{start..end..step}`

---

[Retour](../README.md)