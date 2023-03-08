# URL Parsing

On vous a fourni un fichier texte appelé `urls.txt` qui contient une liste d'URL de sites web. Vous pouvez trouver ce fichier dans la section des ressources pour ce projet.

On vous a demandé d'obtenir les informations d'en-tête reçues lors de la tentative d'accès à la page d'accueil de tous ces sites, et de stocker ces en-têtes dans des fichiers texte individuels.

### Étape 1:
En utilisant la commande `readarray`, créez un tableau d'URL à partir du fichier `urls.txt` fourni.

### Étape 2:
À l'aide d'une boucle `for`, parcourez cet tableau en utilisant la commande curl avec l'option `--head` pour obtenir les en-têtes de chaque URL.

### Étape 3:
Redirigez la sortie de chaque commande `curl` vers un nouveau fichier texte pour chaque URL.

Le nom des fichiers texte devrait être basé sur l'URL.

Par exemple :
- www.facebook.com -> facebook.txt
- www.google.com -> google.txt
- www.thingy.net -> thing.txt

**Astuce**: Consultez la commande `cut` pour découper la partie appropriée de l'URL afin de créer les noms de fichiers.

### Aide supplémentaire
Pour ce projet, vous devrez effectuer des recherches indépendantes à l'aide de la commande `man` pour apprendre comment fonctionnent les commandes `cut` et `curl`. Amusez-vous bien !

Lors de l'utilisation de la commande `cut`, vérifiez les options `-d` et `-f`.

Vous devrez effectuer une redirection de la commande `echo` vers la commande `cut`.