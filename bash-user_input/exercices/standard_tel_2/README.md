# Standard téléphonique amélioré

Vous avez réalisé qu'il y a des informations supplémentaires dont vous avez besoin de la part de vos utilisateurs pour pouvoir configurer efficacement votre standard téléphonique.

Tout d'abord, vous devez fournir à vos utilisateurs un nouveau téléphone pour travailler avec le nouveau système et vous souhaitez donner à vos utilisateurs la possibilité d'avoir soit un téléphone portable soit un téléphone à casque.

Deuxièmement, vous devez savoir dans quel service ils travaillent au sein de l'entreprise.

### Étape 1: 
Vous allez ajouter au script `get_extensions` que vous avez créé précédemment pour cela.

Après avoir demandé à l'utilisateur son nom de famille, vous devrez ajouter deux commandes `select`.

### Étape 2: 
Votre première commande `select` définira une variable pour le type de téléphone avec les options "casque" et "portable" données à l'utilisateur.

Utilisez la variable shell `PS3` pour donner à l'utilisateur une invite appropriée.

Vous utiliserez ensuite la sélection de l'utilisateur dans `echo`.

### Étape 3: 
Ensuite, vous devez ajouter une autre commande `select` pour demander à l'utilisateur son service. Donnez à l'utilisateur les options suivantes: "finance", "ventes", "service client" et "ingénierie".

Encore une fois, utilisez la variable shell `PS3` pour donner à l'utilisateur une invite appropriée, et échoirez sa sélection.

### Étape 4: 
Enfin, vous devez modifier la commande `echo` à la fin du script pour vous assurer que les nouvelles données sont écrites dans le fichier de données.

**Astuce**: N'oubliez pas d'utiliser `break` pour terminer chaque commande `select`.