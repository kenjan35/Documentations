## if __name__ == "__main__":

__name__ est une variable spéciale créée automatiquement par Python.
On utilise if __name__ == "__main__": surtout pour contrôler ce qui doit être exécuté quand un fichier Python est lancé directement, par opposition à quand il est importé.

Par exemple, imaginons un fichier *hello.py* :

```python
def hello() -> None:
    greetings: str = "Hello world"
    print(greetings)

print("Le programme démarre")
```

Ici si on fait:

```bash
python3 hello.py
```

on aura:
```
Le programme démarre
```

Mais si un autre fichier fait :

```python
import hello
```

Python va aussi exécuter :

```python
print("Le programme démarre")
```

Donc on peut avoir du code qui s'exécute simplement parce qu'on a importé le fichier.

Avec if __name__ == "__main__", même si on fait import hello, ça n'affichera plus "Le programme démarre"

```python
def hello():
    print("Hello !")

if __name__ == "__main__":
    print("Le programme démarre")
```

