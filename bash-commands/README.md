# Comment Bash gère les commandes

Lorsque Bash va exécuter notre script, il va, pour chacune des lignes de notre fichier, passer par une série de 5 étapes qui qu'il est intéresssant de connaître dans le but d'améliorer notre compréhension de Bash et donc notre capacité à en réaliser des scripts.

### Etape 1: La Tokenisation

Cette étape sert au shell pour déterminer ce qui est considéré comme une portion de notre commande. Pour fonctionner, le shell va se servir de caractères spéciaux, les méta-caractères, pour délimiter les tokens. On va donc distinguer deux catégorie: Les opérateurs et les mots en fonction de qui est contenu ou non dans des guillemets.

Nous avons ainsi d'un côté les méta-caractères (`|`, `&`, `;`, `()`, `<>` ainsi que `space`, `tab` et `newline`) et de l'autre tout le reste ainsi que les méta-caractères qui auraient pu être mis entre guillemets ou échappés via un backslash `\`. Cet à-côté porte le doux nom de "mot".

Il existe deux grands types d'opérateurs, les opérateurs de **contrôle** et ceux de **redirection**. Par exemple, parmi les opérateurs de contrôle, on trouve `&` qui sert à lancer une commande en tâche de fond. Ces opérateurs ne sont interprétés en tant que tel que s'ils ne sont pas échappées.

Ainsi, dans la commande `echo $name > out.txt`, le shell va interpréter comme suit:
- `>` est un **méta-caractère**, de même que les `space`. 
- On obtiendra donc, sous la forme de plusieurs **mots**: `echo`, `$name` ainsi que `out.txt`. 
- Le caractère de redirection `>`, de son côté, va être interprété comme **opérateur**.

### Etape 2: L'identification de la commande

Cette étape va servir à notre shell pour découper notre ligne en des commandes qui peuvent être de plusieurs types: 
- Les commandes les plus **simples** seront traitées de la sorte: Chaque premier mot de notre token servira à déterminer de quelle commande il s'agit, et tous les autres mots seront ses arguments, le tout se terminant par un opérateur. Par exemple, dans `echo 1 2 3 ` le mot **echo** sera la commande alors que les trois chiffres seront ses trois arguments. Cette ligne sera terminée par le caractère de fin de ligne, invisible pour nous (`;`). Si l'on veut réaliser deux commandes `echo` en une ligne, et obtenir un résultat correct, il nous faudra faire attention à notre syntaxe:

```bash
echo 1 2 3 echo 1 2 3
# 1 2 3 echo 1 2 3

echo 1 2 3; echo 1 2 3
# 1 2 3
# 1 2 3
```

- Les commandes plus **complexes** seront des commandes qui utilisent des structures du type conditionnelle, d'itération, etc... Ces commandes vont commencer par des mots réservés dans le contexte des commandes bash. En reconnaissant ces mots, Bash est capable de comprendre où se trouve le début et la fin d'un bloc de commande de ce type:

```bash
if [[ 2 -gt 1 ]]; then
  echo "Hello world!"
fi
```

Ces commandes peuvent donc, via la nécessité d'un mot correspondant à la fermeture du bloc, être écrites sur plusieurs lignes sans problème dans le but d'en simplifier l'écriture et la lecture.

### Etape 3: Réalisation des Extensions

L'étape suivante est celle dans laquelle le shell va prendre en compte les utilisation des diverses extensions que nous avons vues au chapitre précédent. Une fois ces extensions réalisée et leur contenu remplacé par du texte ou leur résultat, le shell passera à l'étape suivante. Pour ce faire, le shell va réaliser, au sein de cette même étape, quatre stages: 
1. Etape 1: Brace Expansion
2. Etape 2:
  * Parameter Expansion
  * Arithmetic Expansion
  * Command Substitution
  * Tilde Expansion
3. Etape 3: Coupure des mots
4. Etape 4: Le Globbing

Connaissant cet ordre, il est important de faire attention lorsque l'on écrit nos commandes, pour éviter par exemple de demander l'utilisation d'une variable en tant que portée dans une syntaxe à accolades. De même, au sein de la même étape, toutes les extensions se voient accordées la même priorité (ce qui a de l'intérêt dans l'étape 2 de notre shéma).

L'étape de coupure des mots, de son côté, correspond à un processus utilisé par le shell dans le but de transformer le résultat de certaines extensions en une série de mots. 

> Ce processus n'a lieu que dans le cas d'**extension de paramètres**, de la **substitution de commande** ou dans le cadre de l'**extension arithmétique** non échappés par des caractères d'échappement.

### Etape 3.1: La coupure des mots

Les caractères utilisés pour couper les mots sont gouvernés par la variable `IFS` (Internal Field Separator). Cette variable correspond de base aux **espaces**, aux **tabulations** et aux **nouvelles lignes**. Pour pouvoir en apprécier les valeurs, il est possible de le faire via `echo "${IFS@Q}"`

Dans le cadre du script suivant, nous aurons donc la création de 5 fichiers et non par d'un seul:

```bash
numbers="1 2 3 4 5"
touch $numbers
```

Ce résultat est du au fait que notre variable **IFS** contient le caractère d'espace. Pour éviter ce processus, nous pouvons mettre entre double guillemets le contenu de la variable `numbers` dans le but de transformer l'argument envoyé à touch en un seul argument comptenant des espaces:

```bash
numbers="1 2 3 4 5"
touch "$numbers"
```

De même, si l'on le veut, il nous est possible d'altérer le fonctionnement de la variable IFS dans le but de pouvoir transformer certains caractères en des caractères de séparation d'arguments: 

```bash
IFS=","
numbers=1,2,3,4,5
touch $numbers
```

> On peut donc voir qu'il existe une règle simple à connaitre: Si l'on veut que le résultat d'une substitution de commande, d'une extension de paramètre ou de l'extension arithmétique soit traité comme un seul et unique paramètre, il suffit de l'entourer de doubles guillemets.

### Etape 3.2: Le Globbing

Le globbing n'a lieu que sur les mots et non sur les opérateurs. Lorsque le shell va observer les mots, il va analyser la présence des caractères non-echappés `*`, `?` et `[`. Si le mot contient l'un de ces trois caractère, il sera considéré comme un shéma (un pattern). Via ce type de processus, il est possible de placer derrière le caractère `*` n'importe quelle chaine de caractère ou derrière `?` n'importe quel caractère individuel. Via le globbing, le pattern peut ainsi être transformé en une série de mots: 

```bash
rm *
# Ici, via ce pattern, on va remplacer cet argument par absolument tout et n'importe quoi

ls *.txt
# On va avoir un listing de tout ce qui se termine par '.txt'

ls file*.txt
# On va avoir un listing de tout ce qui commence par 'file' se termine par '.txt'

ls file?.txt
# On va avoir un listing de tout ce qui commence par 'file', se poursuit par n'importe quel caractère et se termine par '.txt'

ls file[ab].txt
# On va avoir un listing de tout ce qui commence par 'file', se poursuit par soit 'a', soit 'b' et se termine par '.txt'

ls file[a-e].txt
# On va avoir un listing de tout ce qui commence par 'file', se poursuit par une lettre entre 'a' et 'e' puis se termine par '.txt'
```

### Etape 4: Le retrait des guillemets

Cette étape est, comme sont nom l'indique, un simple retrait des guillemets dans le but de clarifier les commandes. Ce dans le but de préparer le shell pour sont étape finale. Pour ce faire, il va retirer tous les backslashes, les simple et doubles guillemets qui ne résultent pas d'une extension du shell.

- Pour avoir un affichage de `$HOME`, il va nous falloir utiliser par exemple `echo \$HOME`, ce qui va résulter en le retrait du caractère de backslash , qui fut interpété par le shell comme étant présent ici uniquement dans le but de structurer notre commande. 
- Pour obternir le texte `\$HOME`, on peut cette fois-ci faire appel aux simples guillemets `echo '\$HOME'`.

Le placement des guillemets est un concept crucial dans le cadre des commandes bash. Il en existe de trois types et chaqu'un a pour objectif d'altérer une signification particulière à des caractères. 
- L'utilisation du backslash `\` sert à altérer la signification du caractère suivant. 
- Les simples guillemets `' '` dont l'objectif est le retrait de la signification de tous les caractères se trouvant en leur sein.
- Les doubles guillemets `" "` qui ont pour but de retirer toutes les significations à l'exception du caractère de dollars `$` ainsi que des backticks `` ` ``.

```bash
echo John \& Jane

filepath='C:\User\Zhoée\Documents'

filepath="C:\User\\$USER\Documents"
```

### Etape 5: Les Redirections

Dans cette dernière étape, le shell va préparer les commandes et rediriger leurs entrées / sorties / erreurs standard vers les redirections prévues soit par défaut, soit définies au sein des commandes via les opérateurs de contrôle de type `<` ou `>`. Il convient de nous rappeller des différents flux de notre terminal:
- Le flux 0: L'entrée standard (stdin) qui nous permet d'offrir à nos commande un input. 
- Le flux 1: La sortie standard (stdout) va contenir de son côté le résultat d'une commande sans erreur
- Le flux 2: L'erreur standard (stderr) va contenir la sortie d'erreur d'une commande bash

Si l'on veut rediriger l'entrée standard, la syntaxe est la suivante:

```bash
target < command
```

A côté de ça, pour la sortie standard, la syntaxe est la suivante:

```bash
command > target
```

Et enfin, si l'on désire rediriger l'erreur standard:

```bash
command 2> target
```

Il est également possible de rediriger à la fois la sortie et l'erreur standard vers la même cible via:

```bash
command > target
```

Pour un ajout et non un ecrasement de notre cible, on peut ajouter un second chevron après le premier: 

```bash
command_one < base_target | command_two >> main_target 2>> error_target
```

### Et pour finir...

Une fois toutes ces étapes réalisées, le shell va exécuter les commandes, nous permettant d'apprécier le résultat de la commande avant de passer à la ligne suivante de notre script.


---

[Retour](../README.md)