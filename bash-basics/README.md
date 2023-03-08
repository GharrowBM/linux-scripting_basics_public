# Les bases du scripting Bash

Dans le cadre du scripting Linux, il est possible de le réaliser dans une ou plusieurs type de **shell**. Cependant, l'utilisation de **Bash** est privilégiée car outre son nombre de fonctionnalités, il est aussi très rapide. De plus, sa communautéétant très étendue, il est préférable d'apprendre à réaliser du scripting sur Bash.

Un script n'est de son côté ni plus ni moins qu'un fichier contenant des commandes mise en forme de sorte à pouvoir transformer cet aglomérat en un fichier exécutable par Bash. Via l'utilisation des scripts, il est possible de réaliser plusieurs choses sur notre machine de façon très rapide et très aisée. 

Par exemple, au lieu d'enchainer les commandes, on pourrait penser que l'on voudrait, en une commande, transformer toute une hierarchie de fichiers et / ou de dossier en une autre, ou faire un backup sous le format d'un Zip de toute une série d'images, etc...Via l'utilisation du scripting, il est possible de réaliser une **automatisation** des tâches de notre machine.

### La structure des scripts Bash

La première ligne d'un script bash sera toujours la ligne `shbang`. Cette ligne possède une structure propre et nous servira à définir quel est le type de programme qui devra éxecuter le scipt. Pour la mettre en forme, il suffit d'écrire la chaine `#!` suivie du chemin vers l'exécutable devant prendre en compte notre script. Dans notre cas, il s'agira du chemin vers le shell **bash**: 

```bash
#!/bin/bash
```

Si par exemple nous avions voulu faire un script python, il aurait été possible de le faire de la sorte: 

```bash
#!/usr/bin/python3
```

Pour notre premier script, nous allons simplement faire un **Hello World!** classique, suivi de la commande `exit 0` dans le but de faire une sortie sans erreur du script:

```bash
#!/bin/bash

echo "Hello world!"
exit 0
```

Pour rentre notre script exécutable, il va nous falloir modifier les permissions de notre fichier. Pour en changer les permissions, il suffit de faire la commande `chmod +x nom_d_script`.

### Les commentaires

Lorsque l'on veut ajouter des commentaires dans notre script bash, il nous suffit d'ajouter des lignes de caractère qui commencent par le caractère `#`. 

```bash
echo "Hello World!"
# Ceci est un commentaire
exit 0
```

Idéalement, dans le milieu professionnel, les informations à donner en commentaires en début d'un script bash sont:
- Le nom de l'auteur
- La date de création du script
- La date de dernière modification
- Une description sommaire de notre script
- L'utilisation potentielle du script

### La Sécurité de notre script

Lorsque l'on créé un script, il est important de bien connaître les permissions de notre système dans le but de ne pas créer des failles générées par notre script. Par exemple, si l'on donne les droits d'exécution d'un script, il convient de ne pas pour autant donner les droits d'écriture dans le script, sous peine de voir des individus mal intentionnés pouvoir modifier les lignes de commandes et de nous causer des bogues voire même des trous dans notre sécurité. 

Pour donner ç notre fichier de script des permissions adaptées, il va nous falloir user de la commande `chmod`:

Par exemple, pour ne permettre qu'au créateur du script son exécution, on peut utiliser ce type de permissions: 
```bash
chmod 744 nom_du_scripth
```

Pour rapidement connaître les valeurs à donner à notre commande `chmod`, il existe un site assez pratique disponible à [cette adresse](https://chmod-calculator.com/).

### Ajouter nos script à PATH

Pour pouvoir utiliser notre script en tant que ligne de commande, il nous faut utiliser la variable d'environnement PATH. Cette variable d'environnement est utilisée par notre système pour localiser les différents scripts / lignes de commandes que nous pouvons exécuter. Pour rendre nos scripts disponibles, il nous suffit d'ajouter le dossier les contenant dans la variable d'environnement.

Par exemple, nous pouvons créer, dans notre dossier personnel, un sous-dossier `scripts` et ajouter ce dossier à la variable d'environnement: 

```bash
cd ~

mkdir scripts

nano .profile 

# Ajouter à la fin du fichier: export PATH="$PATH:$HOME/scripts"

source .profile # Pour recharger le fichier dans le shell
```

---

[Retour](../README.md)