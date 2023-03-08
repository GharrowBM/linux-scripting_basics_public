# Exercice Backup Script

Votre patron a remarqué que vous effectuez un travail très précieux pour l'entreprise et, pour éviter qu'il ne se perde, il vous a suggéré de créer un script que vous pouvez utiliser pour sauvegarder facilement tous les fichiers de votre répertoire personnel.

Votre patron pense également que ce script sera très utile pour les autres personnes du bureau et souhaite que vous vous assuriez que le script est formaté de manière professionnelle avant de le partager avec vos collègues.

### Étape 1
Créez un script bash appelé `backup_script` dans votre répertoire `~/exercice_back_up/`.

Ce script devrait sauvegarder tous les fichiers de votre répertoire personnel et les sauvegarder dans une archive `.tar`. **Des conseils sont fournis ci-dessous sur la façon de procéder.**

Lors de l'écriture de votre script, n'oubliez pas d'ajouter tous les composants essentiels de votre script:

* La ligne « Shebang »
* Les commandes (voir la section « conseils supplémentaires » ci-dessous)
* Une instruction de sortie avec un code de sortie approprié.

Ainsi que les 5 éléments d'informations professionnelles :
* Auteur
* Date de création
* Dernière modification
* Description
* Utilisation

### Étape 2
Donnez les permissions correctes au script.

Étant donné que le script sera partagé avec d'autres personnes de votre organisation, votre script devrait avoir les permissions suivantes :

* Le propriétaire du fichier (c'est-à-dire vous) doit avoir les permissions de lecture, d'écriture et d'exécution.
* Tout le monde dans le groupe du fichier (c'est-à-dire vos collègues) doit avoir les permissions de lecture et d'exécution. Pour des raisons de sécurité, ils ne doivent pas avoir les permissions d'écriture.
* Tout le monde dans l'organisation ne doit avoir que les permissions de lecture.

Déterminez le code octal correct à utiliser avec la commande `chmod` pour y parvenir.

### Étape 3
Exécutez votre script plusieurs fois pour vérifier qu'il fonctionne.

Vous devriez voir qu'il crée plusieurs sauvegardes pour vous dans votre dossier `~/exercice_back_up`.

### Conseils supplémentaires
Pour créer ce script, vous allez utiliser la commande `tar`.

Si la commande `tar` vous est nouvelle, ne vous inquiétez pas ! Tout ce que vous devez savoir, c'est que la commande `tar` est utilisée pour créer des archives **.tar**, qui sont essentiellement des fichiers **.zip**, mais plus « Linuxy ».

Pour l'instant, nous voulons simplement que vous utilisiez la commande tar pour pratiquer la création de scripts professionnels.

Votre script utilisera la commande ci-dessous (n'hésitez pas à la copier et à la coller) :

```bash
tar -cvf ~/exercice_back_up/my_backup_"$(date +%d-%m-%Y_%H-%M-%S)".tar ~/* 2>/dev/null
```

Cette commande prend le contenu de votre répertoire personnel, le compresse dans une archive **.tar** et enregistre cette archive dans le dossier `~/exercice_back_up`.

La commande nomme également la sauvegarde en fonction de la date et de l'heure actuelles. Par exemple, une sauvegarde effectuée le 12 juillet 2020 à 12h00 serait enregistrée sous le nom `my_backup_12-07-2020_12-00-00.tar`.