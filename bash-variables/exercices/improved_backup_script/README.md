# Backup Script amélioré

Vous utilisez votre script de sauvegarde au travail depuis un certain temps et vous avez découvert quelques problèmes que vous aimeriez résoudre.

Tout d'abord, votre script ne donne aucune sortie à l'utilisateur. Il serait bien d'indiquer à l'utilisateur que le script est en cours d'exécution pour lui donner un peu de tranquillité d'esprit que ses données précieuses sont effectivement sauvegardées.

Deuxièmement, certains de vos collègues ont du mal à utiliser le script car ils n'ont pas de répertoire `bash_course` sur leur système. Pour contourner ce problème, vous souhaitez modifier le script pour qu'il crée une sauvegarde dans le répertoire à partir duquel l'utilisateur exécute le script.

Ce projet comprend cinq étapes.

### Étape 1
Modifiez le script de sauvegarde pour afficher les deux lignes suivantes à l'écran de l'utilisateur lorsque le script est exécuté:

```bash
Bonjour, <Utilisateur>
Je vais maintenant sauvegarder votre répertoire personnel, </chemin/vers/répertoire_personnel>
```

Par exemple:

```bash
Bonjour, Simon
Je vais maintenant sauvegarder votre répertoire personnel, /home/simon/
```

**Remarque**: le nom d'utilisateur de l'utilisateur doit avoir la première lettre en majuscule dans la première ligne du message de salutation.

**Indice 1**: Vous pouvez utiliser la commande `echo` et les variables shell pour y parvenir.

**Indice 2**: Consultez la section du cours sur les "astuces d'extension de paramètres de shell" pour voir comment mettre en majuscule la première lettre du nom d'utilisateur.

### Étape 2
Créez une variable appelée `currentdir` et stockez-y la valeur renvoyée par la commande `pwd`.

La commande `pwd` affiche simplement le chemin d'accès au répertoire de travail actuel de l'utilisateur (c'est-à-dire le répertoire à partir duquel il exécute le script).

**Indice**: Vous devrez utiliser la substitution de commande pour y parvenir.

### Étape 3
Utilisez la commande echo et la variable `currentdir` pour indiquer à l'utilisateur où il a exécuté le script et donc où sa sauvegarde sera enregistrée:

```bash
Vous exécutez ce script à partir de <répertoire_actuel>.
Par conséquent, je vais enregistrer la sauvegarde dans <répertoire_actuel>
```

Par exemple:

```bash
Vous exécutez ce script à partir de /home/simon/bash_course
Par conséquent, je vais enregistrer la sauvegarde dans /home/simon/bash_course
```


### Étape 4
Modifiez la commande `tar` pour sauvegarder le répertoire personnel de l'utilisateur dans le répertoire stocké dans la variable `currentdir`.

Notez que l'option verbeuse (`-v`) doit également être supprimée de la commande `tar` pour que les déclarations echo soient facilement visibles par l'utilisateur.

### Étape 5
Ajoutez une dernière ligne pour que le script indique à l'utilisateur que la sauvegarde est terminée.

Par exemple:

```bash
Sauvegarde terminée avec succès.
```