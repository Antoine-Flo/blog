---
title: "Shell Scripting"
published: 2025-07-07
draft: false
toc: true
description: 'Automate repetitive tasks and streamline your workflow with practical shell scripting examples.'
series: 'Linux'
tags: ['bash']
---

## Basic setup

1. Create a file

```bash
touch my_script.sh
nano my_script.sh   # Create and open the file in the nano text editor
```

2. Add a shebang at the top of the file, then the instructions.

```bash
#!/usr/bin/env bash
echo "Hello, World!"
```

3. Make the file executable

```bash
chmod +x my_script.sh
```

4. Execute the script

```bash
./my_script.sh
```

## Scripting language

### Variables

Variables in bash are denoted with a `$` prefix. For example:

```bash
name="John"
echo "Hello, $name!"
```

### Parameters

Parameters can be passed to a bash script at runtime. 

```bash
./my_script.sh John
```

The value of the parameters can be accessed using the `$1`, `$2`, etc. :

```bash
#!/usr/bin/env bash
echo "Hello, $1!"
```
> Output: Hello, John!


You can also use the variable `read` to get user input and store it in a variable.

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

### Loops

```bash
for i in {1..5}; do ## We can avoid the ; with another line like the next exemple
  echo "Iteration $i"
done
```
> Output: Iteration 1
> Output: Iteration 2
> ...

```bash
for nom in Alice Bob Charlie
    do
        echo "Bonjour, $nom!"
    done
```
> Output: Bonjour, Alice!
> Output: Bonjour, Bob!
> Output: Bonjour, Charlie!

```bash
compteur=1
while [ $compteur -le 2 ]
    do
    echo "Compteur: $compteur"
    ((compteur++))
    done
```
> Output: Compteur: 1
> Output: Compteur: 2

## Exemples

### Check if a a list of input is a file or directory
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

### Change owner of a list of files
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