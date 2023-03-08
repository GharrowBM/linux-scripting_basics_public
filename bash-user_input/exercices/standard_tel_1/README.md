# Standard téléphonique

Vous mettez en place un nouveau standard téléphonique pour le système téléphonique de votre entreprise. Vous devez collecter les numéros de poste actuels de chacun et le code PIN qu'ils veulent utiliser lorsqu'ils effectuent des appels.

Comme il n'y a pas de téléphone interne, vous décidez d'écrire un script bash pour demander cette information à chacun de vos collègues et l'écrire dans un fichier csv pour le traiter ultérieurement.

### Étape 1:
Tout d'abord, vous pouvez créer un script appelé `get_extensions`.

Dans ce script, vous devrez demander à votre utilisateur 4 informations à l'aide de la commande `read`.
- Quel est votre prénom ?
- Quel est votre nom de famille ?
- Quel est votre numéro de poste ?
- Quel code d'accès souhaitez-vous utiliser lors de la composition ?

Vous devez informer l'utilisateur que son numéro de poste et son code d'accès doivent tous deux être exactement de 4 chiffres.

**Remarque**: Vous devez vous assurer que les numéros de poste et les codes PIN ont exactement 4 chiffres. Consultez l'option `-N` dans la documentation de la commande `read`, que vous pouvez accéder en exécutant la commande `help read`

**Astuce**: Lors de la saisie d'informations confidentielles comme les codes d'accès, il est toujours préférable d'empêcher ce que l'utilisateur tape d'apparaître dans le terminal.

**Astuce**: Utilisez la commande echo pour ajouter des lignes vides au besoin pour bien formater l'interface utilisateur.

### Étape 2:
À l'aide de la commande `echo`, vous devez ensuite enregistrer ces informations dans un fichier appelé `extensions.csv` dans le format suivant:

```bash
prénom,nom,poste,accès
```

Enregistrer les données de cette manière permettra d'ouvrir les données dans Microsoft Excel ou un autre logiciel de tableur pour les traiter (essayez-le!)

**Astuce**: assurez-vous que le script ajoute les données au fichier extensions.csv à chaque fois que le script est exécuté.