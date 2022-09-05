## Gestion d'hôtel

On vous demande de concevoir un système de réservations dans un hôtel.

*Note* : le programme, dans cette forme, ne prendra aucune entrée utilisateur (pas de `Scanner` ni autre).

### A. Conception de la classe Chambre

Créez quatre attributs pour cette classe, avec des types appropriés :

- `numéro` de chambre
- `joursRestants` : le nombre de jours restants (payés) pour l'occupant actuel
- `type` : l'une des trois valeurs suivantes : « simple », « double », « suite »
- `nomOccupant` : occupant actuel (null si la chambre est inoccupée)

Écrivez un constructeur pour la classe Chambre. Il doit prendre deux paramètres : le numéro de chambre et le type. Le nombre de jours restants doit être automatiquement mis à `0` et l'occupant à _null_. Pour le type, vérifiez qu'il s'agit bien de l'un des trois types permis. Sinon, mettez le type « simple ».

Écrivez les méthodes suivantes :

- `définirOccupant` prend deux paramètres : le nom de l'occupant et le nombre de jours pendant lesquels il souhaite rester. Elle retourne _vrai_ si l'opération s'est bien passé et _faux_ sinon. Vous devez vérifier si la chambre est déjà louée, auquel cas la méthode retourne faux. Si elle est libre, on met à jour le nom de l'occupant et le nombre de jours et on retourne _vrai_.
- `jourSuivant` décrémente de 1 le nombre de jours restants. Si on arrive à 0, remettre nomOccupant à _null_.
- `toString` retourne une string représentant l'état courant d'une instance. Deux exemples : « *Chambre 123 : double - louée* » ; « *Chambre 456 : suite - libre* »

### B. Conception de la classe Hotel

- Trois attributs : nom de l'hotel, chambres (un tableau de toutes les chambres), nombre de chambres
- Constructeur : trois paramètres - nom de l'hotel, nombre de chambres, nombre d'étages. Après l'initialisation des variables d'instances correspondantes, vous devez instancier le tableau de chambres. Puis vous créerez une instance de Chambre pour chaque élément du tableau. Voici comment créer les chambres :
  - le numéro est une valeur entre 100 et 999. Le premier chiffre correspond à l'étage, et les deux autres doivent s'incrémenter dans l'ordre (100, 101, 102...)
  - cependant, chaque étage aura le même nombre de chambres (vous pouvez considérer que les entrées garantissent que cela est possible)
  - chaque étage aura exactement 4 chambres simples, 1 suite et le reste des chambres à allouer seront toutes doubles (de même, vous pouvez considérer que les entrées garantissent que chaque étage aura au moins 5 chambres)
  - la suite aura le numéro de chambre le plus grand sur l'étage, les chambres simples les numéros les plus petits, et les doubles les numéros intermédiaires
  - récapitulons : si l'hotel a 2 étages et 14 chambres, la répartition devra être exactement celle indiquée ci-dessous :

```
Répartition :
100 (simple), 101 (simple), 102 (simple), 103 (simple), 104 (double), 105 (double), 106 (suite)
200 (simple), 201 (simple), 202 (simple), 203 (simple), 204 (double), 205 (double), 206 (suite)
```

- Écrivez les méthodes suivantes :
  - un _getter_ pour le nombre total de chambres
  - `nbChambresOccupées` doit examiner chacune des chambres et retourner combien d'entre elles sont actuellement occupées
  - `tauxOccupation` retourne un double entre 0 et 100 représentant le pourcentage d'occupation actuel de l'hotel.
  - `louerChambre` prend trois arguments : le type de chambre, le nom du client et le nombre de jours du séjour. Elle retourne un booléen indiquant le succès ou l'échec de l'opération. Parcourez les chambres de l'hôtel et trouvez la première chambre inoccupée qui correspond au type recherché. Enregistrez alors les informations (occupant et temps de séjour) pour cette chambre maintenant louée, et retournez _vrai_. Ne retournez _faux_ que si aucune chambre adéquate n'est trouvée
  - `jourSuivant` passe au jour suivant. La méthode doit répercuter l'information à tous les objets `Chambre` pour la mise à jour des nombres de jours restants dans chaque chambre
  - `toString` retourne une string représentant l'état courant de l'hôtel. Le format attendu est le suivant :

```
Hotel Aifone : 10 % d'occupation. Voici la liste des chambres :
Chambre 100 : simple – louée
Chambre 101 : simple – libre
Chambre 102 : simple – libre
Chambre 103 : simple – louée
Chambre 104 : double – libre
...
```

### C. Tests

Écrivez une méthode de test qui va vérifier le bon fonctionnement de la méthode `tauxOccupation`. De nouveau, pas de `Scanner`, le test doit être automatique : vous pouvez coder « en dur » lors de l'instanciation des objets toutes les valeurs dont vous avez besoin pour le test.

### D. Modification

On souhaite maintenant vérifier que les entrées garantissent effectivement que :

- chaque étage pourra avoir le même nombre de chambres ;
- on aura au moins 5 chambres par étage ;
- pas plus de 100 chambres par étage (sinon pas assez de numéros).

Indiquez quelles sont les modifications à effectuer et à quel endroit pour imposer ces contraintes. En cas de non-respect des contraintes par les entrées, vous devez afficher un message d'erreur correspondant au problème rencontré et sortir immédiatement du programme (`System.exit(0)` arrête immédiatement la JVM et donc le programme).
