### glob

Le module glob permet de rechercher des fichiers ou des dossiers en utilisant des motifs (patterns) avec des caractères spéciaux, un peu comme dans un terminal Linux (*.txt, *.py, etc.).
Il est très pratique lorsque tu ne connais pas exactement le nom d'un fichier.

## 1. Trouver tous les fichiers .py

```python
import glob

fichiers = glob.glob("*.py")
print(fichiers)
```

Résultat :

```sh
['main.py', 'app.py', 'test.py']
```

*.py signifie :
- *→n'importe quelle suite de caractères
- .py→se termine par .py

## 2. Trouver tous les fichiers

```python
import glob

fichiers = glob.glob("*")
print(fichiers)
```

Résultat :

```sh
['main.py', 'app.py', 'test.py', 'data.csv']
```

## 3. Chercher dans un dossier

Imaginons :
```sh
Projet/
│
├── images/
│   ├── logo.png
│   ├── fond.jpg
│   └── chat.png
```

Code :
```python
import glob

images = glob.glob("images/*")
print(images)
```

Résultat :
```python
['images/logo.png', 'images/fond.jpg', 'images/chat.png']
```

## 4. Chercher uniquement les images PNG

```python
import glob

png = glob.glob("images/*.png")
print(png)
```

## 5. Rechercher récursivement

Supposons :
```sh
Projet/
│
├── data/
│   ├── normal/
│   │   ├── Normal_1.csv
│   │   └── Normal_2.csv
│   │
│   └── theft/
│       ├── Theft_1.csv
│       └── Theft_2.csv
```

Pour trouver tous les CSV, même dans les sous-dossiers :

```python
import glob

csv = glob.glob("**/*.csv", recursive=True)
print(csv)
```

Résultat :
```python
[
 'data/normal/Normal_1.csv',
 'data/normal/Normal_2.csv',
 'data/theft/Theft_1.csv',
 'data/theft/Theft_2.csv'
]
```

## 6. Utiliser ?

Le caractère ? représente exactement un caractère.

```python
glob.glob("Normal_?.csv")
```

Résultat :
```python
['Normal_1.csv', 'Normal_2.csv']
```
Normal_10.csv n'est pas trouvé car ? ne remplace qu'un seul caractère.

## 7. Utiliser de crochets []

Supposons :

```sh
Theft_1.csv
Theft_2.csv
Theft_3.csv
Theft_4.csv
glob.glob("Theft_[12].csv")
```
Résultat :
```sh
['Theft_1.csv', 'Theft_2.csv']
```
## 8. Parcourir tous les fichiers trouvés

```python
import glob

for fichier in glob.glob("*.csv"):
    print(fichier)
```
Affichage :
```sh
Normal_1.csv
Normal_2.csv
Theft_1.csv
Theft_2.csv
```
C'est très utile pour traiter automatiquement plusieurs fichiers.

## 9. glob.iglob()

Retourne un itérateur, qui produit les fichiers un par un.
```python
import glob

fichiers = glob.iglob("*.csv")

for fichier in fichiers:
    print(fichier)
```
Cela consomme moins de mémoire lorsqu'il y a des milliers de fichiers.

glob.glob() retourne une liste complète.
Tous les chemins sont chargés en mémoire d'un coup.
