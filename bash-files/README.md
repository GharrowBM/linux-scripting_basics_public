# Gérer les fichiers en Bash

Pour pouvoir gérer de façon optimale les fichiers de notre ordinateur, il convient de savoir utiliser les structures de contrôle de type itérative. Par exemple, la boucle `while`.

De part l'utilisation d'une boucle, il est possible de répéter une certaine quantité d'instructions jusqu'à ce qu'une condition de sortie soit atteinte. Encore une fois, il va nous falloir utiliser des mots-clés pour pouvoir nous en servir. Ces mots protégés sont `while`, `do` et `done`:

```bash
read -p "Entrez un nombre: " number

while [ $number -gt 10 ]; do
  echo $number

  # Il convient de ne pas oublier de modifier la valeur de la variable sous peine d'avoir une boucle infinie
  number=$((number - 1)) 
done
```

Si la condition d'entrée dans la boucle n'est de base pas bonne (l'utilisateur entre directement une valeur inférieure ou égale à 10), alors la boucle ne sera même pas exécutée.

### Gérer les options dans nos scripts

Pour permettre à l'utilisateur d'entrer des options dans le but de potentiellement altérer le fonctionnement de nos scripts, il convient d'utiliser `getopts`, qui est une commande dont l'objectif est l'obtention des options envoyées au script. Pour spécifier que l'utilisateur peut entrer une valeur en supplément de l'option, il faut ajouter le caractère `:` derrière le caractère de l'option. Chaque option va être stockée derrière une variable portant le nom de `OPTARG`. 

Par exemple, imaginons que nous souhaitions créer un script de conversion de température. Il nous faudrait un mode allant de Farenheit vers Celcius et une permettant la conversion inverse:

```bash
# On va récupérer deux options '-f number' et '-c number' qui se verront stockées dans la variable ops

# Pour être sur que toutes les options sont envoyées, on va se servir d'une structure 'while'
while getopts "f:c:" opt; do
  case "$opt" in
    c) result=$(echo "scale=2; ($OPTARG * (9 / 5)) + 32" | bc);;
    f) result=$(echo "scale=2; ($OPTARG - 32) * (5 / 9)" | bc);;

    # Chaque option non valide va être stockée derrière l'option '?', ce qui permet de rendre notre 'default' plus précis dans ce cas précis
    \?);;
  esac

done 

echo "$result"
```

### Itérer dans les fichiers

Pour pouvoir parcourir un fichier ligne par ligne, il est possible de réaliser des boucles de type `read-while`. Ces boucles sont nommées de la sorte car elle utilisent la commande `read` en tant que commande de test. Il convient de faire attention à rediriger, non pas l'entrée standard de la commande `read` mais celle de la boucle `while`, ce qui donne une syntaxe de la sorte:

```bash
while read line; do
  echo $line
done < "$1"
```

Si l'on le veut, il est aussi possible d'avoir recourt à ce qui s'appelle la substitution des processus dans le but de pouvoir envoyer à notre boucle non pas un fichier, mais le résultat d'une commande potentielle (ici une commande listant le contenu de notre dossier personnel): 

```bash
while read line; do
  echo $line
done < <(ls $HOME)
```

---

[Retour](../README.md)