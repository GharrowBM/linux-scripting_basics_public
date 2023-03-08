# Calc Script

On vous a demandé de créer un script bash qui servira de calculatrice de base et vous permettra d'effectuer des calculs arithmétiques simples à partir de la ligne de commande.

La calculatrice doit être capable de faire l'addition, la soustraction, la multiplication et la division, sur un maximum de 9 nombres.

Le premier argument de ligne de commande donné au script contiendra l'opération qui doit être effectuée sur les nombres (soit + ou -).

L'opération choisie sera appliquée à tous les nombres.

Par exemple, si le premier argument de ligne de commande est "+", alors tous les autres arguments de ligne de commande seront additionnés. Si l'utilisateur choisit "-", alors tous les autres arguments de ligne de commande seront soustraits les uns des autres, et ainsi de suite.

Votre script doit être capable d'accepter l'opération en tant que premier argument de ligne de commande, et également accepter jusqu'à 9 nombres (pour un total de 10 arguments de ligne de commande).

**Astuce 1**: Vous devrez utiliser le premier paramètre de position, qui est l'opérateur, plusieurs fois

**Astuce 2**: Vous pouvez utiliser la commande echo pour afficher le résultat de l'expansion arithmétique

**Astuce 3**: + et -, comme tous les opérateurs binaires, nécessitent qu'il y ait un opérande avant et après l'opérateur. "1 +" et "2 -" seuls n'ont aucun sens.
Dans ce cas, que feriez-vous si l'utilisateur voulait seulement ajouter 4 nombres, par exemple?

Pour contourner ce problème, réfléchissez à la façon dont vous pourriez utiliser une astuce d'extension de paramètre comme `${parameter:-word}` pour substituer une valeur par défaut si un paramètre de position donné n'est pas fourni.

Vous pouvez vous référer au [Manuel GNU Bash](https://www.gnu.org/software/bash/manual/bash.html#Shell-Expansions) pour plus de clarté sur l'utilisation de cette astuce d'extension de paramètre particulière: 