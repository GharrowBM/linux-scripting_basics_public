# Memory Logger

C'est l'un de ces jours. Vous avez des problèmes avec un serveur et vous devez enregistrer l'utilisation de la mémoire pour vérifier les problèmes de performance.

Vous devez stocker ce journal dans un emplacement spécifique et vous allez supprimer périodiquement ce journal.

Votre script doit vérifier si le journal existe et y ajouter des données s'il existe afin que vous ne perdiez pas les données existantes. Si le journal n'existe pas, le script doit le créer avec son dossier contenant, si nécessaire.

### Étape 1:
Créez un script bash appelé `memory_logger`

### Étape 2:
Créez une instruction `if`

Cela vérifiera si le dossier `$HOME/performance` existe et s'il n'existe pas, le créera

Si le dossier existe, alors affichez une déclaration confirmant qu'il existe

**Astuce**: Utilisez la commande `mkdir` pour créer le dossier s'il n'existe pas

### Étape 3:
Après votre instruction `if`

Ajoutez la sortie de la commande `free` à `$HOME/performance/memory.log`

**Astuce**: La commande `free` dans Linux affiche l'utilisation actuelle de la mémoire de l'ordinateur.