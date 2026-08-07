### Numpy

1. Créer un tableau

À partir d'une liste :
```python
import numpy as np

a = np.array([1, 2, 3, 4])

print(a)
```

Résultat :
```sh
[1 2 3 4]
```

Matrice :

```python
m = np.array([
    [1, 2],
    [3, 4]
])
```

Résultat :

```sh
[[1 2]
 [3 4]]
```

2. Connaître les propriétés

```python
a = np.array([1, 2, 3, 4])

print(a.shape)
print(a.size)
print(a.dtype)
print(a.ndim)
```

Résultat :
```sh
(4,)
4
int64
1
```

shape → dimensions
size → nombre d'éléments
dtype → type
ndim → nombre de dimensions

3. Créer des tableaux spéciaux

Tous les zéros :

```python
np.zeros(5)
[0. 0. 0. 0. 0.]
```

Tous les uns :

```python
np.ones(5)
```

Même forme qu'un autre tableau :

```python
np.zeros_like(a)
```

Identité :

```python
np.eye(3)
[[1. 0. 0.]
 [0. 1. 0.]
 [0. 0. 1.]]
```

4. Générer des suites

```python
np.arange(0, 10)
[0 1 2 3 4 5 6 7 8 9]
```

Avec un pas :

```python
np.arange(0, 10, 2)
[0 2 4 6 8]
```

Répartition régulière :

```python
np.linspace(0, 1, 5)
[0.   0.25 0.5  0.75 1.  ]
```

5. Sélectionner des éléments
```python
a = np.array([10, 20, 30, 40])
```

Premier :

```python
a[0]
```

Dernier :

```python
a[-1]
```

Plusieurs :

```python
a[1:3]
```

Résultat :

```sh
[20 30]
```

6. Modifier

```python
a[0] = 100
```

7. Opérations mathématiques

Addition :

```python
a + 10
[11 12 13 14]
```

Multiplication :

```python
a * 2
```

Puissance :

```python
a ** 2
```

Division :

```python
a / 2
```

Contrairement aux listes Python, ces opérations s'appliquent à tous les éléments en une seule instruction.

8. Opérations entre tableaux
```python
a = np.array([1,2,3])
b = np.array([4,5,6])
```

Addition :

```python
a + b
```

Résultat :

```sh
[5 7 9]
```

Multiplication élément par élément :

```python
a * b
[ 4 10 18]
```

9. Statistiques
```python
a = np.array([3,8,2,6])
```

Minimum :

```python
a.min()
```

Maximum :

```python
a.max()
```

Moyenne :

```python
a.mean()
```

Somme :

```python
a.sum()
```

Écart-type :

```python
a.std()
```

Variance :

```python
a.var()
```

10. Rechercher

Indice du maximum :

```python
a.argmax()
```

Indice du minimum :

```python
a.argmin()
```

11. Conditions
```python
a = np.array([5,10,15,20])
a > 10
```

Résultat :

```sh
[False False True True]
```

Sélection :

```python
a[a > 10]
```

Résultat :

```sh
[15 20]
```

12. Modifier selon une condition
```python
a[a > 10] = 0
```

Résultat :

```sh
[5 10 0 0]
```

13. Trier
```python
np.sort(a)
```

14. Concaténer
```python
a = np.array([1,2])
b = np.array([3,4])

np.concatenate((a,b))
```

Résultat :

```sh
[1 2 3 4]
```

15. Changer la forme
```python
a = np.arange(12)
a.reshape(3,4)
```

Résultat :

```sh
[[ 0  1  2  3]
 [ 4  5  6  7]
 [ 8  9 10 11]]
```

16. Transposer
```python
m.T
```

Inverse lignes/colonnes.

17. Aplatir
```python
m.flatten()
```

Transforme une matrice en vecteur.

18. Calculs mathématiques
```python
np.sqrt(a)
np.log(a)
np.exp(a)
np.sin(a)
np.cos(a)
```

19. Nombres aléatoires
```python
np.random.rand(5)
```

Entre 0 et 1.

Entiers :

```python
np.random.randint(0,10,5)
```

20. Produit matriciel
```python
A = np.array([[1,2],
              [3,4]])

B = np.array([[5,6],
              [7,8]])

A @ B
```

ou

```python
np.dot(A,B)
```

21. Fenêtres glissantes (ton projet)

Tu utilises déjà ce principe :

```python
fuel = np.array([10,11,12,13,14])

window = fuel[1:4]
```

Résultat :

```sh
[11 12 13]
```

22. Calcul des différences

Très utile dans ton projet.

```python
fuel = np.array([100,98,97,94])

delta = fuel[1:] - fuel[:-1]
```

Résultat :

```sh
[-2 -1 -3]
```

C'est exactement ce qui permet de détecter les baisses de carburant.

23. Empiler des features

Tu utilises aussi :

```python
X = np.column_stack((
    fuel,
    delta,
    np.abs(delta)
))
```

Résultat :

```sh
[[100   0   0]
 [ 98  -2   2]
 [ 97  -1   1]
 [ 94  -3   3]]
```

Chaque ligne représente un échantillon et chaque colonne une feature.

24. Valeur absolue
```python
np.abs(delta)
```

Très utilisé pour ignorer le sens de la variation.

25. Moyenne glissante
```python
window = np.array([10,11,13,12])

window.mean()
```

Résultat :

```sh
11.5
```
