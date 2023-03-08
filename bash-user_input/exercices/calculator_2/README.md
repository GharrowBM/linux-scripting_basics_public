# Calculatrice avancée

En repensant à votre projet de calculatrice et ayant maintenant appris sur les paramètres spéciaux, vous réalisez que les paramètres spéciaux permettraient de créer un script beaucoup plus propre que les paramètres de position.

Un gros avantage est que, en raison de leur nature générale, les paramètres spéciaux permettraient à votre calculatrice de fonctionner sur un nombre infini de nombres, plutôt que d'être limitée à utiliser le nombre de paramètres que vous avez référencé dans le script.

Vous seriez également en mesure de fournir plusieurs opérateurs différents entre chaque nombre avec cette solution.

Vous décidez de modifier votre script de calculatrice pour utiliser des paramètres spéciaux à la place!

Modifiez le script de calculatrice que nous avons créé dans le projet de paramètres de position précédent, et remplacez les paramètres de position par un paramètre spécial qui fera le même travail tout seul.

Le script résultant devrait permettre à un utilisateur d'exécuter des calculs en utilisant un nombre illimité de nombres et plus d'un opérateur, par exemple:

`./calculatrice 1 + 4 - 6.`

**Astuce 1**: Vous voulez utiliser le paramètre spécial qui étendra chaque paramètre de position à son propre mot séparé.

**Astuce 2**: Ne réfléchissez pas trop! Il est possible de faire ce script avec juste 1 ligne de code!