## 1. Créer une date spécifique

```python
dt.datetime(year, month, day, hour=0, minute=0, second=0)
```

On peut aussi ajouter microsecond, tzinfo (fuseau horaire).

## 2. Obtenir la date/heure actuelle

```python
dt.datetime.now()      # Date et heure locales
dt.datetime.utcnow()   # Date et heure UTC
dt.datetime.today()    # Similaire à now()
```

## 3. Opérations sur les dates (timedelta)

Quand on soustrait deux datetime, on obtient un objet **timedelta** :

```python
diff = now - past_date  # Résultat : datetime.timedelta
```

Un timedelta représente une durée et possède ces méthodes :
* total_seconds() → durée totale en secondes (float)
* days → nombre de jours
* seconds → secondes restantes (après les jours)
* microseconds → microsecondes restantes

## 4. Formatter l'affichage

**strftime()** = "string format time" (datetime → string)

```python
dt.datetime.now().strftime('%b %d %Y')
```

### Codes de format courants :

* %Y → année sur 4 chiffres (2026)
* %y → année sur 2 chiffres (26)
* %m → mois (01-12)
* %b → mois abrégé (Jan, Feb, Mar...)
* %B → mois complet (January, February...)
* %d → jour du mois (01-31)
* %H → heure 24h (00-23)
* %M → minutes (00-59)
* %S → secondes (00-59)

## 5. Parser une chaîne en datetime

**strptime()** = "string parse time" (string → datetime)

```python
date_str = "27 Oct 2026"
date_obj = dt.datetime.strptime(date_str, '%d %b %Y')
```

Exemple complet pratique :

```python
import datetime as dt

# Créer une date
birthday = dt.datetime(1990, 5, 15, 14, 30)

# Date actuelle
now = dt.datetime.now()

# Calculer l'âge
age = now - birthday
print(f"Âge en jours : {age.days}")
print(f"Âge en années : {age.days / 365.25:.1f}")

# Formater l'affichage
print(f"Birthday : {birthday.strftime('%d/%m/%Y at %H:%M')}")
```

*Note : float(diff_sec) est redondant car total_seconds() retourne déjà un float. On peut écrire directement **diff_sec dans le f-string.***