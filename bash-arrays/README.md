# Les Arrays (Tableaux) en Bash

Les Arrays les plus communs dans le monde de Bash sont sans doute les Arrays indéxés. Ces Arrays sont en réalité des série de valeurs regroupées derrière une seule et unique variable et dont chaque sous-ensemble possède un index permettant d'accéder à une valeur particulière directement. Ainsi, au lieu de devoir créer une cinquantaine de variables pour stocker 50 prénoms, on peut imaginer créer un Array portant le nom de `prenoms` et qui contiendra les 50 prénoms, chacun des prénom étant ensuite accessible via son index. **L'indexage d'un array commencera à 0**.

```bash
numbers=(1 2 3 4 5)

echo $numbers
# Par défaut, on va obtenir l'index 0 => 1

echo ${numbers[2]}
# On aura la 3ème valeur => 3

echo ${numbers[@]}
# De la sorte, on obtient toutes les valeurs d'un coup => 1 2 3 4 5 

echo ${numbers[@]:1}
# Il est possible d'utiliser l'extension des paramètres pour réaliser un offset de l'Array => 2 3 4 5

echo ${numbers[@]:1:2}
# De même qu'un slicing => 2 3 
```

Dans le cas où l'on souhaite modifier les valeurs d'un array, il est aussi très facile de le faire en ciblant directement l'index souhaité. Pour par exemple ajouter une valeur à notre array, il va falloir cependant lui envoyer non pas une valeur, mais un tableau contenant la valeur. La syntaxe se présente de la sorte. Il est ainsi possible d'ajouter plusieurs valeurs d'un coup également:

```bash
numbers+=(6)

numbers+=(7 8 9 10)
```

Pour retirer une valeur, il va falloir utiliser cette fois-ci la commande `unset` ainsi que l'index que l'on souhaite retirer, de la sorte:

```bash
unset numbers[4]
```

Attention cependant, lorsque l'on supprime un index, le tableau ne se réorganise pas de lui-même pour recréer une continuité dans les indices. Ceci est vérifiable via l'affichage `echo ${!numbers[@]}` qui permet l'affichage non pas des valeurs mais des indices par ajout du caractère `!` en début de la syntaxe.

Pour changer un élément en particulier, la syntaxe est des plus simple: 

```bash
numbers[1]=7
```

### La commande readarray

Via la commande `readarray`, il est possible par exemple de générer des tableaux depuis des fichiers. Sont fonctionnement est assez simple car il consiste en la transformation de tout ce qu'elle lira dans l'entrée standard en un tableau. 

En observant les caractères masqués dans la lecture des élémentss d'un array créé à partir d'un fichier, via la syntaxe `echo ${nom_array[@]@Q}`, il est possible de remarquer que les éléments ne seront pas clairement définis et porteront en leur sein le caractère de nouvelle ligne. Pour éviter cela, il est possible d'ajouter l'option `-t` à la commande **readarray** de la sorte:

```bash
readarray -t array_name < file.txt
```

Si l'on veut pouvoir stocker dans une variable de type array le résultat de la commande **ls**, il n'est malheureusement pas possible d'avoir recourt au piping. Cependant, via la substition du processus, il est possible de transformer une commande en un faux fichier ainsi compatible avec notre commande **readarray**. La syntaxe se présente de la sorte:

```bash
<(commande) 
# La commande sera transformée en un faux fichier, qui pourra être envoyé via une redirection à l'entrée standard d'une autre commande
```

Notre script se présentera ainsi de la sorte:

```bash
readarray -t files < <(ls path/to/files)
```

### Itérer sur un Array

Les tableaux sont des structure très facilement compatible avec une boucle itérative, et la majorité des boucles servent d'ailleurs à parcourir un array de données dans le but de les traiter une par une très rapidement. Pour ce faire, on peut utiliser une boucle de type `for` dont les mots-clés réservés sont `for`.

```bash
for element_name in 1 2 3; do
  echo $element_name
done
```

Imaginons maintenant que nous souhaitions faire un script créant une série de fichiers. Ce script pourrait prendre la forme suivante:

```bash
readarray -t files < "$1"

for file in "${files[@]}"; do
  if [ -f "$file" ]; then
    echo "$file already exists"
  else
    touch "$file"
    echo "$file was created"
  fi
done
```

---

[Retour](../README.md)