---
title: "Les Essentiels de Python"
published: 2025-09-04
draft: false
toc: true
description: "Référence complète Python couvrant la syntaxe, les structures de données, le contrôle de flux, la gestion de fichiers et les bibliothèques principales—parfait pour les développeurs expérimentés qui passent à Python."
tags: ['python', 'programming', 'tutorial']
series: 'Code'
---

Python est un langage de programmation de haut niveau et interprété. Ce guide couvre les concepts essentiels pour les développeurs qui migrent vers Python ou cherchent une référence complète.

## Installation

### Linux (Debian/Ubuntu)
```bash
sudo apt update
sudo apt install python3 python3-pip
python3 --version  # Vérifier l'installation
```

### macOS
```bash
# Utiliser Homebrew
brew install python

# Ou télécharger depuis python.org
```

### Windows
Téléchargez depuis [python.org](https://www.python.org/downloads/) ou utilisez le Windows Store. Assurez-vous de cocher "Ajouter au PATH" pendant l'installation.

```cmd
python --version  # Vérifier l'installation
pip --version     # Gestionnaire de paquets
```

## Syntaxe de Base

### Fonction Print
Afficher des données dans le terminal avec diverses options de formatage.

```python
print("Hello, World!")
print("Value: ", 42)
print("Multiple", "values", "separated")

# Sortie formatée
name, age = "Alice", 25
print(f"Name: {name}, Age: {age}")
print("Name: {}, Age: {}".format(name, age))

# Contrôler le comportement de sortie
print("No newline", end="")
print(" continues here")
print("Item1", "Item2", sep=" | ")  # Séparateur personnalisé
```

### Commentaires
Documenter le code avec des commentaires sur une ligne ou multi-lignes.

```python
# Commentaire sur une ligne
print("Hello, World!")  # Commentaire en ligne

"""
Commentaire multi-lignes (docstring)
Utilisé pour des explications détaillées
ou la documentation de fonctions
"""

'''
Syntaxe multi-lignes alternative
utilisant des guillemets simples
'''
```

### Variables
Le typage dynamique permet aux variables de changer de type. Aucune déclaration explicite n'est nécessaire.

```python
# Assignation de base
a = 5
name = "Alice"

# Assignation multiple
b, c = 1, 2
x = y = z = 0

# Échanger les variables
a, b = b, a

# Changements de type autorisés
a = 5        # int
a = "Hello"  # maintenant string
a = [1, 2]   # maintenant list

# Constantes (convention : majuscules)
PI = 3.14159
MAX_SIZE = 100
```

### Types de Données
Python prend en charge plusieurs types de données intégrés avec inférence automatique.

```python
# Types numériques
x = 5               # int
y = 3.14            # float
z = 2 + 3j          # nombre complexe

# Booléen
is_valid = True     # bool (True/False)
is_empty = False

# Chaînes
name = "Alice"      # str
text = 'Single quotes work too'
multiline = """Line one
Line two
Line three"""

# Type None
value = None        # NoneType

# Vérification et conversion de type
print(type(x))              # <class 'int'>
print(isinstance(x, int))   # True

# Conversion de type
str(42)         # "42"
int("42")       # 42
float("3.14")   # 3.14
bool(1)         # True
bool(0)         # False
```

## Manipulation de Données

### Opérations sur les Chaînes
Manipulation complète des chaînes avec découpage, formatage et méthodes.

```python
text = "Hello World!"

# Découpage [début:fin:pas]
text[0:5]       # "Hello"
text[6:]        # "World!"
text[:5]        # "Hello"
text[-1]        # "!"
text[-6:-1]     # "World"
text[::2]       # "HloWrd"

# Formatage de chaînes
name = "Alice"
age = 30
greeting = f"Hello, {name}. You are {age}."
formatted = "Hello, {}. You are {}.".format(name, age)
old_style = "Hello, %s. You are %d." % (name, age)

# Méthodes de chaînes
len(text)           # 12
text.upper()        # "HELLO WORLD!"
text.lower()        # "hello world!"
text.title()        # "Hello World!"
text.strip()        # Supprimer les espaces
text.replace("World", "Python")  # "Hello Python!"

# Test de chaînes
text.startswith("Hello")  # True
text.endswith("!")        # True
text.isdigit()            # False
"123".isdigit()           # True

# Division et jointure
words = text.split()             # ["Hello", "World!"]
" ".join(words)                  # "Hello World!"
"Hello,World,Python".split(",")  # ["Hello", "World", "Python"]

# Alignement
text.ljust(15)      # "Hello World!   "
text.rjust(15)      # "   Hello World!"
text.center(15)     # " Hello World!  "
```

### Opérations Numériques
Opérations arithmétiques et fonctions mathématiques.

```python
a, b = 10, 3

# Arithmétique de base
c = a + b    # 13 Addition
c = a - b    # 7  Soustraction
c = a * b    # 30 Multiplication
c = a / b    # 3.333... Division (float)
c = a // b   # 3  Division entière (int)
c = a % b    # 1  Modulo (reste)
c = a ** b   # 1000 Exponentiation

# Assignation composée
c = 5
c += 2       # c = c + 2, maintenant 7
c -= 1       # c = c - 1, maintenant 6
c *= 3       # c = c * 3, maintenant 18
c /= 2       # c = c / 2, maintenant 9.0

# Fonctions intégrées
abs(-5)        # 5
round(3.7)     # 4
round(3.7, 1)  # 3.7
min(1, 2, 3)   # 1
max(1, 2, 3)   # 3
sum([1, 2, 3]) # 6

# Module math
import math
math.sqrt(16)    # 4.0
math.ceil(3.2)   # 4
math.floor(3.8)  # 3
math.pi          # 3.141592653589793
```

## Structures de Données

### Listes
Collections ordonnées et modifiables supportant différents types de données.

```python
# Création
fruits = ["apple", "banana", "cherry"]
mixed = [1, "apple", 3.14, True]
numbers = list(range(5))        # [0, 1, 2, 3, 4]
empty = []

# Accès et découpage
first = fruits[0]               # "apple"
last = fruits[-1]               # "cherry"
subset = fruits[1:3]            # ["banana", "cherry"]

# Modification
fruits.append("orange")          # Ajouter à la fin
fruits.insert(1, "blueberry")    # Insérer à l'index
fruits.extend(["mango", "kiwi"]) # Ajouter plusieurs éléments

# Suppression
fruits.pop()                    # Supprimer et retourner le dernier
fruits.pop(1)                   # Supprimer à l'index
fruits.remove("banana")         # Supprimer la première occurrence
del fruits[0]                   # Supprimer par index

# Propriétés et recherche
len(fruits)                     # Compter les éléments
"apple" in fruits               # Vérifier l'appartenance
fruits.index("cherry")          # Trouver l'index
fruits.count("apple")           # Compter les occurrences

# Tri et inversion
numbers = [3, 1, 4, 1, 5]
numbers.sort()                  # [1, 1, 3, 4, 5] (sur place)
sorted(numbers, reverse=True)   # [5, 4, 3, 1, 1] (nouvelle liste)
numbers.reverse()               # Inverser sur place

# Compréhensions de listes
squares = [x**2 for x in range(5)]            # [0, 1, 4, 9, 16]
evens = [x for x in range(10) if x % 2 == 0]  # [0, 2, 4, 6, 8]
```

### Tuples
Collections ordonnées et immuables idéales pour des jeux de données fixes.

```python
# Création
coordinates = (10.0, 20.0)
point = 1, 2, 3              # Parenthèses optionnelles
single = (42,)               # Élément unique nécessite une virgule
empty = ()

# Accès (comme les listes)
x = coordinates[0]           # 10.0
y = coordinates[1]           # 20.0

# Déballage
x, y = coordinates           # x=10.0, y=20.0
first, *rest = (1, 2, 3, 4)  # first=1, rest=[2, 3, 4]

# Propriétés
len(coordinates)             # 2
2 in (1, 2, 3)               # True

# Cas d'utilisation
rgb = (255, 128, 0)                 # Valeurs de couleur
person = ("Alice", 25, "Engineer")  # Données de type enregistrement
```

### Dictionnaires
Paires clé-valeur pour mapper des relations et structurer les données.

```python
# Création
person = {
    "name": "Alice",
    "age": 30,
    "city": "Wonderland"
}
empty = {}
from_keys = dict.fromkeys(["a", "b"], 0)  # {"a": 0, "b": 0}

# Accès et modification
name = person["name"]           # "Alice"
age = person.get("age", 0)      # 30 (avec défaut)
person["job"] = "Engineer"      # Ajouter nouvelle clé
person["age"] = 31              # Mettre à jour existant

# Méthodes
keys = person.keys()            # dict_keys(['name', 'age', 'city', 'job'])
values = person.values()        # dict_values(['Alice', 31, 'Wonderland', 'Engineer'])
items = person.items()          # Paires clé-valeur

# Appartenance et suppression
"name" in person                   # True
del person["city"]                 # Supprimer clé
removed = person.pop("job", None)  # Supprimer et retourner

# Compréhensions de dictionnaires
squares = {x: x**2 for x in range(5)}  # {0: 0, 1: 1, 2: 4, 3: 9, 4: 16}
filtered = {k: v for k, v in person.items() if len(str(v)) > 3}
```

### Ensembles (Sets)
Collections non ordonnées d'éléments uniques.

```python
# Création
colors = {"red", "green", "blue"}
numbers = set([1, 2, 2, 3, 3])     # {1, 2, 3} - doublons supprimés
empty = set()                      # {} crée un dict, pas un set

# Opérations
colors.add("yellow")               # Ajouter élément
colors.remove("red")               # Supprimer (erreur si non trouvé)
colors.discard("purple")           # Supprimer (pas d'erreur si non trouvé)

# Opérations d'ensembles
set1 = {1, 2, 3}
set2 = {3, 4, 5}
union = set1 | set2                # {1, 2, 3, 4, 5}
intersection = set1 & set2         # {3}
difference = set1 - set2           # {1, 2}
symmetric_diff = set1 ^ set2       # {1, 2, 4, 5}

# Test d'appartenance (très rapide)
3 in colors                        # True
colors.issubset({1, 2, 3, 4})      # Vérifier si sous-ensemble
```

## Structures de Contrôle

### Instructions Conditionnelles
Exécuter du code basé sur des conditions booléennes avec if/elif/else.

```python
x = 10

# Conditionnelles de base
if x > 0:
    print("Positive")
elif x < 0:
    print("Negative")
else:
    print("Zero")

# Opérateurs de comparaison
x == 5      # Égal
x != 5      # Différent
x > 5       # Supérieur à
x >= 5      # Supérieur ou égal à
x < 5       # Inférieur à
x <= 5      # Inférieur ou égal à

# Opérateur ternaire (if en ligne)
status = "positive" if x > 0 else "non-positive"

# Conditions multiples
if 0 < x < 100:             # Comparaisons en chaîne
    print("Between 0 and 100")

# Valeurs vraies/fausses
if []:          # False (liste vide)
if "":          # False (chaîne vide)
if 0:           # False (zéro)
if None:        # False
if [1, 2]:      # True (liste non vide)
```

### Opérateurs Logiques
Combiner plusieurs conditions avec and, or, not.

```python
x, y = 5, -3

# Opérateurs logiques de base
x > 0 and y > 0         # False (les deux doivent être True)
x > 0 or y > 0          # True (au moins un doit être True)
not x > 0               # False (négation)

# Évaluation en court-circuit
x > 0 and expensive_function()  # expensive_function appelée seulement si x > 0

# Conditions complexes
if (x > 0 and y > 0) or (x < 0 and y < 0):
    print("Same sign")

# Opérateurs d'identité et d'appartenance
x is None                       # Vérification d'identité
x is not None
"apple" in ["apple", "banana"]  # Appartenance
"grape" not in ["apple", "banana"]
```

### Boucles
Itérer sur des séquences et répéter l'exécution de code.

```python
# Boucles for avec range
for i in range(5):              # 0, 1, 2, 3, 4
    print(i)

for i in range(2, 8, 2):        # 2, 4, 6 (début, fin, pas)
    print(i)

# Boucles for avec séquences
fruits = ["apple", "banana", "cherry"]
for fruit in fruits:
    print(fruit)

# Enumerate pour index et valeur
for index, fruit in enumerate(fruits):
    print(f"{index}: {fruit}")

# Contrôle de boucle
for i in range(10):
    if i == 3:
        continue            # Passer à l'itération suivante
    if i == 7:
        break               # Sortir de la boucle
    print(i)
# Sortie: 0 1 2 4 5 6

# Déballage dans les boucles
pairs = [(1, 'a'), (2, 'b'), (3, 'c')]
for number, letter in pairs:
    print(f"{number}: {letter}")

# Boucles while
count = 0
while count < 5:
    print(count)
    count += 1

# Clause else (exécutée si la boucle se termine sans break)
for i in range(3):
    print(i)
else:
    print("Loop completed")

# Boucles imbriquées
for i in range(3):
    for j in range(2):
        print(f"({i}, {j})")
```

### Fonctions
Blocs de code réutilisables avec paramètres et valeurs de retour.

```python
# Fonction de base
def greet(name):
    return f"Hello, {name}!"

# Paramètres par défaut
def power(base, exponent = 2):
    return base ** exponent

# Arguments nommés
def describe_pet(name, animal_type="dog"):
    print(f"Pet: {name} ({animal_type})")

describe_pet("Max")                             # Utilise la valeur par défaut
describe_pet(animal_type="cat", name="Fluffy")  # Ordre des mots-clés

# Arguments variables
def sum_all(*args):             # Tuple d'arguments
    return sum(args)

sum_all(1, 2, 3, 4)            # 10

def print_info(**kwargs):       # Dictionnaire d'arguments nommés
    for key, value in kwargs.items():
        print(f"{key}: {value}")

print_info(name="Alice", age=30, city="Paris")

# Fonctions lambda (anonymes)
square = lambda x: x ** 2
add = lambda x, y: x + y
numbers = [1, 2, 3, 4, 5]
squared = list(map(square, numbers))        # [1, 4, 9, 16, 25]
evens = list(filter(lambda x: x % 2 == 0, numbers))  # [2, 4]

# Docstrings*
# Elles sont utilisées pour décrire la fonction et ses paramètres.
def calculate_area(radius):
    """
    Calculer l'aire d'un cercle.
    
    Args:
        radius (float): Le rayon du cercle
        
    Returns:
        float: L'aire du cercle
    """
    return 3.14159 * radius ** 2
```

### Gestion d'Exceptions
Gérer les erreurs élégamment avec les blocs try/except.

```python
# Gestion d'exceptions de base
try:
    result = 10 / 0
except ZeroDivisionError:
    print("Cannot divide by zero!")
finally:
    print("Finally block always executed")

# Plusieurs types d'exceptions
try:
    value = int(input("Enter a number: "))
    result = 10 / value
except ValueError:
    print("Invalid number format")
except ZeroDivisionError:
    print("Cannot divide by zero")

# Capturer plusieurs exceptions
try:
    with open('file.txt', 'r') as file:
        data = file.read()
        number = int(data)
except (FileNotFoundError, ValueError) as e:
    print(f"Error: {e}")

# Gestionnaire d'exceptions générique
try:
    risky_operation()
except Exception as e:
    print(f"Unexpected error: {e}")

# Bloc else (exécuté s'il n'y a pas d'exception)
try:
    result = 10 / 2
except ZeroDivisionError:
    print("Division error")
else:
    print(f"Success: {result}")

# Lever des exceptions
def validate_age(age):
    if age < 0:
        raise ValueError("Age cannot be negative")
    return age
```

### Gestionnaires de Contexte (instruction with)
Gestion automatique des ressources assurant un nettoyage approprié.

```python
# Gestion de fichiers avec fermeture automatique
with open('file.txt', 'r') as file:
    content = file.read()
    # Fichier automatiquement fermé en sortant du bloc

# Fichiers multiples
with open('input.txt', 'r') as infile, open('output.txt', 'w') as outfile:
    data = infile.read()
    outfile.write(data.upper())

# Gestionnaire de contexte personnalisé
from contextlib import contextmanager

@contextmanager
def timer():
    import time
    start = time.time()
    print("Timer started")
    try:
        yield
    finally:
        end = time.time()
        print(f"Elapsed: {end - start:.2f}s")

with timer():
    # Opération qui prend du temps
    time.sleep(1)
```

## Programmation Orientée Objet

### Classes et Objets
Définir des types de données personnalisés avec attributs et méthodes.

```python
# Classe de base
class Person:
    def __init__(self, name, age):      # Constructeur
        self.name = name                # Attribut d'instance
        self.age = age
    
    def greet(self):                    # Méthode d'instance
        return f"Hello, I'm {self.name}"
    
    def have_birthday(self):
        self.age += 1

# Créer des objets
person1 = Person("Alice", 30)
person2 = Person("Bob", 25)

print(person1.greet())                  # "Hello, I'm Alice"
person1.have_birthday()
print(person1.age)                      # 31

# Attributs et méthodes de classe
class Circle:
    pi = 3.14159                        # Attribut de classe
    
    def __init__(self, radius):
        self.radius = radius
    
    def area(self):
        return Circle.pi * self.radius ** 2
    
    @classmethod
    def from_diameter(cls, diameter):   # Constructeur alternatif
        return cls(diameter / 2)
    
    @staticmethod
    def is_valid_radius(radius):        # Méthode utilitaire
        return radius > 0

# Héritage
class Employee(Person):                 # Hérite de Person
    def __init__(self, name, age, job_title):
        super().__init__(name, age)     # Appeler le constructeur parent
        self.job_title = job_title
    
    def greet(self):                    # Redéfinition de méthode
        return f"Hello, I'm {self.name}, a {self.job_title}"

employee = Employee("Charlie", 35, "Developer")
print(employee.greet())                 # "Hello, I'm Charlie, a Developer"
```

## Opérations sur les Fichiers

### Lecture et Écriture de Fichiers
Gérer les opérations d'entrée/sortie de fichiers en toute sécurité.

```python
# Lecture de fichiers
with open('data.txt', 'r') as file:
    content = file.read()               # Lire tout le fichier
    
with open('data.txt', 'r') as file:
    lines = file.readlines()            # Liste de lignes
    
with open('data.txt', 'r') as file:
    for line in file:                   # Itérer ligne par ligne
        print(line.strip())

# Écriture de fichiers
with open('output.txt', 'w') as file:
    file.write("Hello, World!")
    
data = ["line1", "line2", "line3"]
with open('output.txt', 'w') as file:
    file.writelines(f"{line}\n" for line in data)

# Modes de fichiers
# 'r' - lecture (par défaut)
# 'w' - écriture (écrase)
# 'a' - ajout
# 'x' - création exclusive
# 'b' - mode binaire
# 't' - mode texte (par défaut)

# Travailler avec les chemins
import os
from pathlib import Path

# Utiliser le module os
current_dir = os.getcwd()
file_path = os.path.join(current_dir, 'data', 'file.txt')
if os.path.exists(file_path):
    os.remove(file_path)

# Utiliser pathlib (approche moderne)
path = Path('data') / 'file.txt'
if path.exists():
    content = path.read_text()
    path.unlink()                       # Supprimer le fichier
```

## Environnements Virtuels
Isoler les dépendances de projet pour éviter les conflits.

```bash
# Créer un environnement virtuel
python -m venv myenv

# Activer l'environnement
# Linux/macOS:
source myenv/bin/activate
# Windows:
myenv\Scripts\activate

# Installer des paquets
pip install requests numpy

# Sauvegarder les dépendances
pip freeze > requirements.txt

# Installer depuis requirements
pip install -r requirements.txt

# Désactiver l'environnement
deactivate
```

## Bibliothèque Standard
Modules essentiels inclus avec Python pour les tâches courantes.

### sys - Interface Système
```python
import sys

# Informations système
sys.platform            # 'linux', 'win32', 'darwin'
sys.version             # Informations de version Python
sys.version_info        # Tuple nommé avec parties de version

# Contrôle du programme
sys.exit(0)             # Sortir avec code de statut
sys.argv                # Liste des arguments de ligne de commande

# Flux d'entrée/sortie
print("Error!", file=sys.stderr)
sys.stdout.write("Direct output\n")

# Manipulation des chemins
sys.path.append('/custom/module/path')
```

### os - Interface Système d'Exploitation
```python
import os

# Opérations de répertoire
os.getcwd()                     # Répertoire de travail actuel
os.chdir('/path/to/directory')  # Changer de répertoire
os.listdir('.')                 # Lister le contenu du répertoire
os.makedirs('path/to/dir', exist_ok=True)  # Créer des répertoires

# Opérations de fichiers
os.rename('old.txt', 'new.txt')
os.remove('file.txt')           # Supprimer le fichier
os.path.exists('file.txt')      # Vérifier si le chemin existe
os.path.isfile('file.txt')      # Vérifier si c'est un fichier
os.path.isdir('directory')      # Vérifier si c'est un répertoire

# Variables d'environnement
home = os.environ.get('HOME', '/tmp')
os.environ['CUSTOM_VAR'] = 'value'
```

### subprocess - Gestion des Processus
```python
import subprocess

# Exécuter des commandes
result = subprocess.run(['ls', '-l'], capture_output=True, text=True)
if result.returncode == 0:
    print(result.stdout)
else:
    print("Error:", result.stderr)

# Exécuter avec le shell
subprocess.run('echo "Hello" > output.txt', shell=True)

# Différentes méthodes d'exécution
subprocess.call(['python', 'script.py'])           # Attendre la fin
subprocess.Popen(['python', 'server.py'])          # Non bloquant
```

### pathlib - Gestion Moderne des Chemins
```python
from pathlib import Path

# Création et manipulation de chemins
path = Path('data') / 'files' / 'document.txt'
path.mkdir(parents=True, exist_ok=True)     # Créer des répertoires

# Opérations de fichiers
path.write_text('Hello, World!')
content = path.read_text()
path.unlink()                               # Supprimer le fichier

# Propriétés de chemin
path.name           # 'document.txt'
path.stem           # 'document'
path.suffix         # '.txt'
path.parent         # Path('data/files')
```

### datetime - Date et Heure
```python
from datetime import datetime, date, timedelta

# Date et heure actuelles
now = datetime.now()
today = date.today()

# Formatage
formatted = now.strftime('%Y-%m-%d %H:%M:%S')
parsed = datetime.strptime('2023-12-25', '%Y-%m-%d')

# Arithmétique
tomorrow = today + timedelta(days=1)
week_ago = now - timedelta(weeks=1)
```

### json - Traitement JSON
```python
import json

# Python vers JSON
data = {'name': 'Alice', 'age': 30}
json_string = json.dumps(data)
with open('data.json', 'w') as f:
    json.dump(data, f, indent=2)

# JSON vers Python
parsed_data = json.loads(json_string)
with open('data.json', 'r') as f:
    loaded_data = json.load(f)
```

### random - Nombres Aléatoires
```python
import random

random.randint(1, 10)           # Entier aléatoire entre 1 et 10
random.random()                 # Float aléatoire entre 0 et 1
random.choice(['a', 'b', 'c'])  # Choix aléatoire dans une séquence
random.shuffle([1, 2, 3, 4])    # Mélanger la liste sur place

# Échantillonnage aléatoire
random.sample([1, 2, 3, 4, 5], 3)  # Échantillon de 3 éléments sans remplacement
```

## Bibliothèques Externes
Packages tiers populaires étendant les capacités de Python.

### requests - Bibliothèque HTTP
```bash
pip install requests
```

```python
import requests

# Requête GET
response = requests.get('https://api.github.com/users/octocat')
data = response.json()
print(response.status_code)     # 200

# Requête POST
payload = {'key': 'value'}
response = requests.post('https://httpbin.org/post', json=payload)

# Avec headers et paramètres
headers = {'Authorization': 'Bearer token'}
params = {'page': 1, 'per_page': 10}
response = requests.get('https://api.example.com/data', 
                       headers=headers, params=params)
```

### numpy - Calcul Numérique
```bash
pip install numpy
```

```python
import numpy as np

# Création de tableaux
arr = np.array([1, 2, 3, 4, 5])
matrix = np.array([[1, 2], [3, 4]])
zeros = np.zeros((3, 3))
ones = np.ones((2, 4))
range_arr = np.arange(0, 10, 2)     # [0, 2, 4, 6, 8]

# Opérations sur les tableaux
arr * 2                             # Multiplication élément par élément
arr + 10                            # Addition élément par élément
np.sum(arr)                         # Somme de tous les éléments
np.mean(arr)                        # Moyenne
np.max(arr)                         # Valeur maximale
```

### pandas - Analyse de Données
```bash
pip install pandas
```

```python
import pandas as pd

# Création de DataFrame
data = {'name': ['Alice', 'Bob', 'Charlie'],
        'age': [25, 30, 35],
        'city': ['New York', 'London', 'Tokyo']}
df = pd.DataFrame(data)

# Opérations sur les données
df.head()                           # 5 premières lignes
df.describe()                       # Résumé statistique
df[df['age'] > 30]                  # Filtrer les lignes
df.groupby('city').mean()           # Grouper par ville

# Opérations de fichiers
df.to_csv('data.csv', index=False)
df_loaded = pd.read_csv('data.csv')
```

### matplotlib - Graphiques
```bash
pip install matplotlib
```

```python
import matplotlib.pyplot as plt

# Graphique simple
x = [1, 2, 3, 4, 5]
y = [2, 4, 6, 8, 10]
plt.plot(x, y)
plt.xlabel('X values')
plt.ylabel('Y values')
plt.title('Simple Line Plot')
plt.show()

# Graphiques multiples
plt.subplot(2, 1, 1)
plt.plot(x, y)
plt.subplot(2, 1, 2)
plt.bar(x, y)
plt.show()
```

### psutil - Informations Système
```bash
pip install psutil
```

```python
import psutil

# Surveillance système
psutil.cpu_percent(interval=1)      # Utilisation CPU
psutil.virtual_memory().percent     # Utilisation mémoire
psutil.disk_usage('/').percent      # Utilisation disque

# Informations des processus
for proc in psutil.process_iter(['pid', 'name', 'cpu_percent']):
    if proc.info['cpu_percent'] > 1.0:
        print(proc.info)
```
