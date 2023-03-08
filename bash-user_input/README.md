# Gérer les entrées Utilisateur

Dans le cas du scripting Bash, il est important de permettre à l'utilisateur de notre script d'en modifier le fonctionnement de par l'ajout de certains de ses choix. Ces choix peuvent être les arguments de notre script. Pour que notre script puisse travailler de la même façon que la commande `cd`, par exemple, il nous faudra utiliser la fonctionnalité des paramètres positionnels.

### Les paramètres positionnels

Les arguments positionnels sont ceux que l'on utilise dans ce cas de figure:

```bash
script_name argA argB argC
```

Leur ordre est important car le mécanisme des paramètres positionnels se base sur leur position / leur ordre d'entrée. La chose est assez simple, car il suffit de demander via la syntaxe de l'extension des paramètres le paramètre 1, 2, 3, etc...

```bash
echo "Je m'appelle $1, j'ai $2 ans et je porte un pull de couleur $3"
```

Il ne nous reste plus qu'a lancer notre script avec une ligne de commande pouvant avoir cette syntaxe:

```bash
our_script Martin 47 bleue
# "Je m'appelle Martin, j'ai 47 ans et je porte un pull de couleur bleue
```

Suite à cet utilisation du shell pour créer des arguments positionnels basés sur les nombres, il est par conséquent impossible d'affecter à une variable numérique une valeur. Ainsi, la ligne suivante est impossible: 

```bash
2="Ma Valeur"
```

### Les paramètres spéciaux

Il existe des paramètres spéciaux dans un script bash: `$#` et `$0`. Leur objectif est de permettre des fonctionnalités particulières à notre Shell. Il n'est pas possible d'en changer leur valeur, qui sera calculée par le Shell en fonction de notre script et non attribuée par nous. 
- `$#` sert à connaitre le nombre d'arguments positionnels qui ont été envoyés au Shell. ON peut imaginer s'en servir pour vérifier qu'il y a bien un nombre pair d'arguments, par exemple.
- `$0` sert de son côté à connaitre, dans un terminal classique, le nom de notre Shell. Dans le cadre d'un script, il permet de connaître le nom du script provoquant son apparition. Il est ainsi utile pour envoyer à l'utilisateur un message d'erreur.
- `$@` est un paramètre spécial qui permet d'accéder d'un seul coup tous les paramètres envoyés à notre script, le tout séparé par un espace. Chaque paramètre sera ainsi considéré comme son propre mot. Via son entourage par deux guillemets, on peut imaginer que le résultat serait un seul mot (`"$1 $2 $3 $4..."`), mais il n'en est rien. Le résultat de cette opération sera **l'entourage de chaque paramètre par des guillemets, le tout encore séparé par un espace** (`"$1" "$2" "$3" "$4"...`). De la sorte, on peut empêcher le word splitting d'avoir lieu sur chaque paramètre envoyé à notre script mais tout de même les travailler sous la forme de plusieurs mots.
- `$*` de son côté offre la même fonctionnalité que le `$@` non positionné entre des guillemets. Il est cependant possible de se servir de ce paramètre différemment via les doubles guillemets, car il prend en compte la valeur de la variable IFS pour séparer les mots contrairement à son homologue **$@**. Ainsi, si l'on réalise un script de la sorte:

```bash
IFS=,
echo "$*"
```

et que l'on provoque son exécution avec l'envoi des trois paramètres ci-dessous, on aura un résultat sous la forme de paramètres séparés par des virgules:

```bash
mon_script 1 2 3
# 1,2,3
```

### La commande read

La commande `read` est une commande permettant à l'utilisateur d'entrer des valeurs, par exe:mple suite à une question que lui aurait posé le terminal durant l'exécution du script. Cette valeur sera stockée dans une variable portant le doux nom de `REPLY` par défaut. Si l'on ajoute des arguments à la commande `read`, alors ces arguments deviennent les noms des variables qui seront stockées dans le résultat de la commande:

```bash
read A B

# L'utilisateur tape 'Hello World'

echo $A
# Hello

echo $B
# World
```

Il est cependant préférable d'offrir un prompt à l'utilisateur plutôt que de lui présenter un curseur clignottant qui n'aura sans doute pas d'autre sens pour lui qu'une erreur potentielle. Pour ce faire, il est possible d'utiliser l'option `-p` dans la commande read:

```bash
read -p "Votre message: " nom_variable
```

A côté de cela, il est possible d'utiliser une option, `-t` pour éviter que le script reste en pause trop longtemps dans le cas d'un manque de réaction de l'utilisateur. La valeur a donnée sera un nombre de seconde. Il est aussi possible d'utiliser l'option `-s` pour ne pas révéler ce que l'utilisateur tape (Attention, la variable sera toujours stockée en texte brut dans le Shell): 

```bash
read -t 5 -p -s "Votre message: " nom_variable
```

### La commande select

De son côté, la commande `select` est une autre façon d'obtenir des informations utilisateur, par exemple dans le cadre de la réalisation d'un menu. Sa syntaxe est assez particulière:

```bash
select variable_name in valueA valueB valueC valueD;
do
echo "Your choice: $variable_name"
```

Le choix se fera via l'entrée d'un nombre correspondant au menu généré. Si l'on entre une valeur n'étant pas dans les choix proposés, aucune valeur ne sera envoyée à la variable. Par défaut, l'utilisation de `select` va causer la création d'une boucle infinie. Il nous est ainsi nécessaire d'utiliser en plus la commande `break` pour causer la fin de cette boucle.

```bash
select variable_name in valueA valueB valueC valueD;
do
echo "Your choice: $variable_name"
break
done
```

Si l'on souhaite changer le prompt envoyé à l'utilisateur lors d'un choix multiple de la sorte, il nous faut modifier la valeur de la variable d'environnement `PS3`.

---

[Retour](../README.md)