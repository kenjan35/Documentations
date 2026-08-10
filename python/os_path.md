# os.path

"os.path" est un module de Python qui permet de manipuler les chemins de fichiers et de dossiers sans avoir à écrire les séparateurs (/ sous Linux/macOS ou \ sous Windows) à la main.

1. os.path.join()
   Permet de construire un chemin correctement.

```python
import os

chemin = os.path.join("Documents", "Python", "main.py")
print(chemin)
```

2. os.path.exists()

Vérifie si un fichier ou un dossier existe.

```python
import os

print(os.path.exists("main.py"))
```

Résultat :
```sh
True
```
ou
```sh
False
```

3. os.path.isfile()

Vérifie si le chemin correspond à un fichier.

```python
import os

print(os.path.isfile("main.py"))
```
Si main.py existe :
```sh
True
```
Si c'est un dossier ou qu'il n'existe pas :
```sh
False
```

4. os.path.isdir()

Vérifie si le chemin correspond à un dossier.

```python
import os

print(os.path.isdir("Documents"))
```

Résultat :
```sh
True
```

5. os.path.basename()

Récupère uniquement le nom du fichier.

```python
import os

chemin = "Documents/Python/main.py"

print(os.path.basename(chemin))
```

Résultat :
```sh
main.py
```

6. os.path.dirname()

Récupère uniquement le dossier.

```python
import os

chemin = "Documents/Python/main.py"

print(os.path.dirname(chemin))
```

Résultat :
```sh
Documents/Python
```

7. os.path.splitext()

Sépare le nom du fichier et son extension.

```python
import os

nom, extension = os.path.splitext("photo.png")

print(nom)
print(extension)
```
