# Ajouter de la logique dans nos scripts

Pour gérer la logique de nos scripts, il est tout d'abord important de savoir que lorsque l'on entre une ou plusieurs commandes sur une seule ligne, ces commandes se retrouvent regroupées derrière une liste de commandes et ce même s'il n'y a qu'une seule commande. Pour créer des listes personnalisées, il est possible de le faire via des opérateurs de liste qui sont: 
- `&`: Cette commande va lancer la première commande en tâche de fond alors que celle à droite de l'opérateur va être lancée immédiatement. Cet opérateur est utile dans le cas où l'on veut créer de l'asynchronisme dans notre script
- `;` va créer le lancement des commandes dans l'ordre gauche-droite. Il faudra attendre la fin de la première commande pour exécuter la seconde commande. Cet opérateur a le même effet que d'écrire nos deux commandes sur deux lignes différentes.
- `&&` permet de lancer la première commande puis la seconde uniquement dans le cas où la première commande a réussi.
- `||` permet de lancer la second commande uniquement dans le cas où la première a echoué.

### Les commandes de test

A côté de cela, il existe ce que l'on appelle des commandes de test. Via ces commandes, il est possible de réaliser des tests conditionnels qui seront essentiels à la création de blocs de constrôle de type `if` par la suite.

Les commandes de test on pour but de comparer différentes informations. Il en existe plusieurs en fonction de ce que l'on veut tester et de quel type de données doit être testé. Si un test renvoi comme résultat `true` alors le test se terminera avec un status `exit 0`, tout comme une commande ayant fonctionné. De même, si le test est `false`, le code de sortie sera `1`.

La syntaxe pour un test est d'utiliser des crochets:

```bash
[ 4 -eq 4 ] ; echo $? # Est-ce-que 4 est égale à 4 ?
# 0 car 4 vaut bien 4

[ 1 -eq 4 ] ; echo $? # Est-ce-que 1 est égale à 4 ?
# 1 car 1 n'est pas égal à 4
```

Il existe ainsi plusieurs opérateurs pour les nombres tels que:
- `-eq` => Egal à 
- `-ne` => N'est pas égal à 
- `-gt` => Plus grand que 
- `-lt` => Plus petit que
- `-ge` => Plus grand ou égal à
- `-le` => Plus petit ou égal à 

Lorsque l'on travaille avec les chaines de caractères, les opérateurs sont:
- `=` => Est-ce-que les chaines sont les mêmes ?
- `!=` => Est-ce-que les chaines sont différentes ?
- `-z` => Est-ce-que La chaine à droite est vide ?
- `-n` => Est-ce-que La chaine à droite n'est pas vide ?

Enfin, il est possible de réaliser ce genre d'opération sur des fichiers:
- `-e` => Pour vérifier que le chemin existe.
- `-f` => Pour vérifier que le chemin est un fichier classique.
- `-x` => Pour vérifier que le chemin existe et qu'il est possible de l'exécuter.
- `-r` => Pour vérifier que le chemin existe et qu'il est possible de le lire.
- `-w` => Pour vérifier que le chemin existe et qu'il est possible d'y écrire.

### La structure If...Then...Fi

Si l'on le veut, il est possible d'exécuter des commandes seulement si une certaine condition est passée. Pour ce faire, il nous faut recourir à des blocs de contrôle de type conditionnels. Pour en créer, il est possible d'avoir recours à `if` et `fi`, ces derniers étant des mots réservés du Shell. Leur fonctionnement passe par la comparaison du code de sortie, qui doit être de **0** pour que la condition soit passée. La syntaxe est donc:

```bash
if [[ 2 -gt 1 ]]; then 
  echo "2 est bien plus grand que 1"
fi
```

Si l'on le veut, il est possible d'utiliser également le mot-clé `else` pour qu'une autre portion de commandes soient exécutées dans le cadre où la condition n'est pas vérifiée:

```bash
x=1

if [[ $x -gt 1 ]]; then 
  echo "x est bien plus grand que 1"
else
  echo "x n'est pas plus grand que 1"
fi
```

Il est aussi possible de faire plusieurs embranchements via l'utilisation du mot-clé `elif`:

```bash
age=19

if [[ $age -gt 21 ]]; then 
  echo "Vous êtes majeur aux USA"
elif [[ $age -gt 18 ]]; then
  echo "Vous êtes majeur en France"
else 
  echo "Vous êtes mineur"
fi
```

A partir de ce moment là, il convient de bien faire attention à l'ordre de nos tests pour éviter des problèmes de logique. Dans notre exemple, on utilise une condition basée sur la supériorité ou l'égalité à une valeur numérique, et les tests d'ordonnent en allant de la valeur la plus grande à la plus petite. L'inverse aurait causé le test de supériorité à 18 d'être vrai avant de tester si l'on était bien supérieur à 21, ce qui aurait été une faute de logique.

Il est aussi possible de combiner les conditions via les opérateurs `&&` et `||`. Via leur utilisation, on peut créer des tests qui peuvent tester plusieurs choses à la fois avant de retourner un code de sortie positif ou négatif:

```bash
a=$(cat file1.txt)
b=$(cat file2.txt)
c=$(cat file3.txt)

if [[$a = $b ] && [ $b = $c ]]; then 
  rm file2.txt file3.txt
else
  echo "File did not match"
fi
```

### La structure Case

A côté de la structure de type **if**, il est possible d'utiliser la structure `case` pour créer un embranchement logique. Les mots-clés réservés sont `case` and `esac`. Cette structure de contrôle est particulièrement utile dans le cas où l'on aurait eu une multitude de structures du type `elif` en usant de la structure vue précédemment. Elle se présente de la sorte: 

```bash
read -p "Veuillez entrer un nombre: " number

case "$number" in 
  [0-9]) echo "Vous avez entré un nombre à un chiffre";;
  [0-9][0-9]) echo "Vous avez entré un nombre à deux chiffres";;
  [0-9][0-9][0-9]) echo "Vous avez entré un nombre à trois chiffres";;
  *) echo "Votre nombre comporte plus de 3 chiffres";;
esac
```

---

[Retour](../README.md)