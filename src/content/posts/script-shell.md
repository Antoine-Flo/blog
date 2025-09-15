---
menuTitle: "Script Shell"
title: "Comment écrire des scripts shell"
published: 2025-07-07
draft: false
toc: true
description: 'Automatise les tâches répétitives et optimise ton workflow avec des exemples pratiques de scripts shell.'
series: 'Linux'
tags: ['bash']
---

Les scripts shell permettent d'exploiter le shell comme un langage de programmation déjà préinstallé sur la plupart des distributions Linux. Ils vous permettront de créer des automatisations basiques.

## Configuration de base

1. Créer un fichier

```bash
touch my_script.sh
nano my_script.sh   # Créer et ouvrir le fichier dans l'éditeur de texte nano
```

2. Ajouter un shebang en haut du fichier, puis les instructions.

```bash
#!/usr/bin/env bash
echo "Hello, World!"
```

3. Rendre le fichier exécutable

```bash
chmod +x my_script.sh
```

4. Exécuter le script

```bash
./my_script.sh
```

## Langage de script

### Variables

Les variables en bash sont précédées d'un préfixe `$`. Par exemple :

```bash
name="John"
echo "Hello, $name!"
```

### Paramètres

Les paramètres peuvent être passés à un script bash lors de l'exécution.

```bash
./my_script.sh John
```

La valeur des paramètres peut être accédée en utilisant `$1`, `$2`, etc. :

```bash
#!/usr/bin/env bash
echo "Hello, $1!"
```
> Sortie : Hello, John!


Tu peux aussi utiliser la commande `read` pour obtenir une saisie utilisateur et la stocker dans une variable.

```bash
#!/usr/bin/env bash
echo "Enter your name:"
read name
echo "Hello, $name!"
```

### Conditions

```bash
#!/usr/bin/env bash
if [ "$1" == "John" ]; then 
  echo "Hello, John!"
else
  echo "Hello, stranger!"
fi
```

### Boucles

```bash
for i in {1..5}; do ## On peut éviter le ; avec une nouvelle ligne comme dans l'exemple suivant
  echo "Iteration $i"
done
```
> Sortie : Iteration 1
> Sortie : Iteration 2
> ...

```bash
for nom in Alice Bob Charlie
    do
        echo "Bonjour, $nom!"
    done
```
> Sortie : Bonjour, Alice!
> Sortie : Bonjour, Bob!
> Sortie : Bonjour, Charlie!

```bash
compteur=1
while [ $compteur -le 2 ]
    do
    echo "Compteur: $compteur"
    ((compteur++))
    done
```
> Sortie : Compteur: 1
> Sortie : Compteur: 2

## Exemples

### Vérifier si une liste d'entrées est un fichier ou un répertoire
```bash
#!/usr/bin/env bash
if [[ "$#" -eq 0 ]]; then
        echo "Usage: ./checkType.sh <path>"
        exit 1
fi

for arg in "$@"; do
        if [ -f "$arg" ]; then
                echo "$arg is a file"
        elif [ -d "$arg" ]; then
                echo "$arg is a directory"
        else
                echo "$arg does not exist or is neither a file nor a folder"
        fi
done
```

### Changer le propriétaire d'une liste de fichiers
```bash
#!/usr/bin/env bash

echo "Files to update :"
read files

echo "New owner and group :"
read new_owner

for file in $files; do

        if [[ ! -f "$file" ]]; then
                echo "$file is not a file"
                continue
        fi
        current_owner=$(ls -l "$file" | awk '{print $3}')

        if [[ "$current_owner" != "$new_owner"  ]]; then
                sudo chown "$new_owner" "$file"
                echo "$file owner $current_owner changed to $new_owner"
        fi
done
```