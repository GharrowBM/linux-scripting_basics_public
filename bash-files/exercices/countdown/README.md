# Exercice Countdown

Nous voulons construire un minuteur qui compte à rebours à partir du nombre spécifié fourni par l'utilisateur.

L'utilisateur utilisera des options de ligne de commande pour fournir un nombre de minutes et un nombre de secondes pour le minuteur.

Le script devra alors calculer le nombre total de secondes et effectuer un compte à rebours, affichant le nombre de secondes restantes jusqu'à 0.

### Étape 1:
Vous devez ajouter `getopts` à votre script pour fournir deux options à votre utilisateur.

Le script doit accepter une option `-m` pour les minutes et une option `-s` pour les secondes.

Vous devrez également utiliser une expansion arithmétique pour calculer le nombre total de secondes et enregistrer cette valeur dans une variable appelée `total_seconds`.

### Étape 2:
Vous devez ensuite créer une boucle `while` qui affiche le nombre total de secondes restantes, une fois par seconde, jusqu'à ce qu'il ne reste plus de secondes.

Remarque : Vous pouvez utiliser la commande "`sleep 1s`" pour faire en sorte que votre boucle fasse une pause d'une seconde avant de continuer.

### Étape 3:
Enfin, lorsque le script se termine, assurez-vous d'afficher la phrase "Time's Up!" avec `echo`.