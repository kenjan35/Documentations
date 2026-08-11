1. Sauvegarder et charger des objets

C'est la fonctionnalité la plus connue.

```python
import joblib

joblib.dump(objet, "objet.joblib")

objet = joblib.load("objet.joblib")
```

Utile pour :

* modèles ML
* tableaux NumPy
* dictionnaires
* paramètres
* objets Python complexes

2. Sauvegarder des modèles de Machine Learning

Très utilisé avec scikit-learn.

```python
joblib.dump(model, "model.joblib")
```

Puis :

```python
model = joblib.load("model.joblib")
```

Cela permet de faire :

```
Entraînement
     ↓
   model
     ↓
joblib.dump()
     ↓
model.joblib
     ↓
joblib.load()
     ↓
Prédiction
```

3. Compression des fichiers

joblib peut compresser les objets sauvegardés.

```python
joblib.dump(data, "data.joblib", compress=3)
```

Tu peux utiliser différents niveaux de compression.

```python
compress=0
```

→ aucune compression

```python
compress=3
```

→ compression modérée

```python
compress=9
```

→ compression forte

La compression peut réduire considérablement la taille des fichiers contenant de gros tableaux NumPy.

4. Calcul parallèle

joblib permet d'exécuter plusieurs tâches en parallèle avec :

```python
from joblib import Parallel, delayed
```

Exemple :

```python
from joblib import Parallel, delayed

def carre(x):
    return x * x

resultats = Parallel(n_jobs=2)(
    delayed(carre)(x)
    for x in range(10)
)

print(resultats)
```

Résultat :

```
[0, 1, 4, 9, 16, 25, 36, 49, 64, 81]
```

Ici :

```python
n_jobs=2
```

signifie qu'on demande à joblib d'utiliser 2 workers.

Tu peux aussi utiliser :

```python
n_jobs=-1
```

pour utiliser tous les CPU disponibles.

