### Pandas

- columns : return all column's real name
- to_numpy : convert into numpy ndarray

```sh
import pandas as pd

df = pd.read_csv("Normal_1.csv")

# It will print pandas.core.frame.DataFrame. A DataFrame is like an Excel sheet in memory.
print(type(df))

# It will print first lines to check if file loads successfully.
print(df.head())

print(df.columns)

# fuel become a Series pandas. A Series is a column.
fuel = df["Fuel Volume"]

# It will print pandas.core.series.Series
print(type(fuel))

# Then we need to convert the Series into NumPy ndarray. Now type(fuel) will return ndarray
fuel = fuel.to_numpy()
```

1. Lire des données

Créer un DataFrame à partir d'un fichier.
```python
import pandas as pd

df = pd.read_csv("data.csv")
```

Afficher les premières lignes :

```python
print(df.head())
```

```sh
   Nom   Age  Ville
0  Alice  25  Paris
1  Bob    31  Lyon
2  Eva    28  Nice
```

2. Explorer les données

Connaître la structure du DataFrame.

Nombre de lignes et colonnes :

```python
df.shape
```

```sh
(1000, 5)
```

Nom des colonnes :

```python
df.columns
```

3. Sélectionner des données

Une colonne :

```python
df["Age"]
```

Plusieurs colonnes :

```python
df[["Nom", "Age"]]
```

Une ligne :

```python
df.iloc[0]
```

Une cellule :

```python
df.loc[0, "Age"]
```

 La méthode loc (par étiquette)
- Principe : On appelle les lignes ou les colonnes par leur nom exact.
- Inclusif : Dans un découpage (slice) de type 0:3, la dernière valeur est comprise dans le résultat.
- Filtre : Elle accepte les conditions logiques (les booléens).
- Exemple : df.loc[0, 'Nom'] sélectionne la ligne d'étiquette 0 et la colonne nommée 'Nom'.

 La méthode iloc (par position)
- Principe : On appelle les lignes ou les colonnes par leur position en chiffres entiers (0 pour la première, 1 pour la deuxième, etc.).
- Exclusif : Dans un découpage (slice) de type 0:3, la dernière valeur n'est pas comprise (elle s'arrête à 2).
- Exemple : df.iloc[0, 0] sélectionne la première ligne et la première colonne du tableau.

4. Filtrer des données

Les personnes de plus de 30 ans :

```python
df[df["Age"] > 30]
```

Deux conditions :

```python
df[(df["Age"] > 30) & (df["Ville"] == "Paris")]
```

5. Trier

Par âge :

```python
df.sort_values("Age")
```

Ordre décroissant :

```python
df.sort_values("Age", ascending=False)
```

6. Ajouter une colonne
```python
df["Age x2"] = df["Age"] * 2
```

Résultat :

```sh
Nom    Age   Age x2
Alice   25      50
Bob     31      62
```

7. Modifier des valeurs
```python
df["Age"] = df["Age"] + 1
```

Ou seulement certaines lignes :

```python
df.loc[df["Age"] < 18, "Age"] = 18
```

8. Supprimer

Une colonne :

```python
df.drop(columns=["Ville"])
```

Une ligne :

```python
df.drop(index=3)
```

9. Renommer

Colonnes :

```python
df.rename(columns={"Age": "Âge"})
```

10. Gérer les valeurs manquantes

Compter :

```python
df.isna().sum()
```

Supprimer :

```python
df.dropna()
```

Remplacer :

```python
df.fillna(0)
```

Ou

```python
df.fillna(df["Age"].mean())
```

11. Supprimer les doublons

```python
df.drop_duplicates()
```

12. Convertir un type

Texte → entier

```python
df["Age"] = df["Age"].astype(int)
```

Date :

```python
df["Date"] = pd.to_datetime(df["Date"])
```

13. Calculer

Moyenne :

```python
df["Age"].mean()
```

Maximum :

```python
df["Age"].max()
```

Minimum :

```python
df["Age"].min()
```

Somme :

```python
df["Age"].sum()
```

Écart-type :

```python
df["Age"].std()
```

14. Grouper

Par ville :

```python
df.groupby("Ville")["Age"].mean()
```

Résultat :

```sh
Paris    29.4
Lyon     34.7
Nice     25.8
```

15. Compter

Nombre de personnes par ville :

```python
df["Ville"].value_counts()
```

16. Fusionner

Deux DataFrames :

```python
df = pd.merge(df1, df2, on="ID")
```

17. Concaténer
```python
df = pd.concat([df1, df2])
```

Très utile pour réunir les données des fichiers.

18. Appliquer une fonction
```python
df["Age"] = df["Age"].apply(lambda x: x + 5)
```

Ou avec une fonction personnelle :

```python
def carre(x):
    return x * x

df["Age²"] = df["Age"].apply(carre)
```

19. Itérer

Par lignes :

```python
for _, row in df.iterrows():
    print(row["Age"])
```
La méthode iterrows() renvoie deux valeurs à chaque itération :
* l'index de la ligne
* la ligne elle-même (sous forme de Series)

En Python, _ signifie par convention :
"Je reçois cette valeur, mais je ne vais pas l'utiliser."

20. Sauvegarder

En CSV :

```python
df.to_csv("resultat.csv", index=False)
```

En Excel :

```python
df.to_excel("resultat.xlsx", index=False)
```
