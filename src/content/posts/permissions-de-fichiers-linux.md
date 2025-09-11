---
title: "Les droits"
published: 2025-07-07
draft: false
toc: true
description: "Comprendre les permissions de fichiers Linux et le contrôle d'accès utilisateur, comment sécuriser correctement vos fichiers et répertoires."
series: 'Linux'
tags: ['security']
---

Linux offre un ensemble puissant d'outils pour gérer les droits utilisateur et les permissions. Nous donnons des droits minimaux aux utilisateurs et processus pour limiter les dégâts potentiels.

## Les trois types de droits

1. Lecture (r) : Permet à un utilisateur de voir le contenu d'un fichier ou répertoire.
2. Écriture (w) : Permet à un utilisateur de modifier ou supprimer un fichier ou répertoire.
3. Exécution (x) : Permet à un utilisateur d'exécuter un fichier ou d'accéder à un répertoire.

## Les trois groupes de permissions

### Utilisateurs
Chaque utilisateur individuel sur un système Linux a un identifiant utilisateur unique (UID) et des permissions associées. Les comptes utilisateur peuvent être créés, modifiés et supprimés en utilisant divers outils en ligne de commande.

Il y a un utilisateur spécial nommé root. L'utilisateur root a un accès illimité à toutes les commandes et fichiers sur un système Linux. Comme bonne pratique, il est recommandé d'utiliser le compte root seulement quand c'est absolument nécessaire.

### Groupe
Vous pouvez organiser les utilisateurs en groupes pour gérer les permissions plus facilement. Chaque fichier et répertoire a un groupe associé, et les utilisateurs peuvent être ajoutés ou supprimés de ces groupes.

Un utilisateur peut être dans plusieurs groupes. Dans ce cas, l'utilisateur hérite des permissions de tous les groupes auxquels il appartient.

Un fichier a toujours un propriétaire (utilisateur) et un groupe propriétaire. Le propriétaire a toutes les permissions, tandis que le groupe et les autres ont des permissions limitées.

### Autres
Les autres font référence à tous les utilisateurs qui ne sont pas le propriétaire d'un fichier ou membre du groupe du fichier. Ils ont le moins de permissions.

## Gérer les groupes et utilisateurs

### Obtenir des infos sur l'utilisateur et le groupe

```bash
cut -d: -f1 /etc/passwd  # Lister tous les utilisateurs
cut -d: -f1 /etc/group  # Lister tous les groupes

id [username]  # Obtenir l'ID utilisateur (uid), l'ID groupe (gid), et les appartenances aux groupes
groups [username]  # Lister tous les groupes dont l'utilisateur est membre
```

### Créer un utilisateur

```bash
sudo useradd [username]
```

### Créer un groupe

```bash
sudo groupadd [groupname]
```

### Ajouter un utilisateur à un groupe

```bash
# Lors de la création d'un nouvel utilisateur
sudo useradd -m -G [groupname] [username]  # -m crée le répertoire home
# Ajouter un utilisateur existant à un groupe
sudo usermod -aG [groupname] [username] # -a ajouter, garder les groupes précédents
```

### Supprimer un utilisateur ou un groupe

```bash
sudo userdel [username]  # Supprimer un utilisateur
sudo groupdel [groupname]  # Supprimer un groupe
sudo userdel -r [username]  # Supprimer un utilisateur et son répertoire home
```

### Définir un mot de passe pour un utilisateur

```bash
sudo passwd [username]
sudo chpasswd [username]  # Changer le mot de passe
```

## Gérer les droits

### Vérifier les droits 

#### Notation symbolique

Vous pouvez vérifier les permissions d'un fichier ou répertoire en utilisant la commande `ls -l`. Cela affichera une liste de fichiers et répertoires avec leurs permissions, propriétaires et groupes.

```bash
-rw-r--r-- 1 user group 0 Jul  7 12:00 file.txt
-rwxr-xr-x 1 bob devops 0 Jul  7 12:00 script.sh
 \ /\ /\ /
  v  v  v
  |  |  droits des autres utilisateurs (o)
  |  |
  |  droits des utilisateurs appartenant au groupe (g)
  |
  droits du propriétaire (u)
 
r : read | w : write | x : execute
```

Les droits sont divisés par 3. Le premier caractère représente le type de fichier '-' pour fichier, 'd' pour répertoire, et 'l' pour lien symbolique. Les trois premiers caractères représentent les permissions du propriétaire, les trois suivants les permissions du groupe, et les trois derniers les permissions des autres.

Pour le `file.txt`, le propriétaire (user) a les permissions `rw-` lecture et écriture, le groupe a les permissions de lecture `r--`, et les autres ont les permissions de lecture. Pour le `script.sh`, le propriétaire a les permissions de lecture, écriture et exécution, le groupe a les permissions de lecture et exécution, et les autres ont les permissions de lecture et exécution.

#### Notation octale

En plus de la notation précédente, Linux supporte aussi la notation octale pour les permissions de fichiers. Dans cette notation, chaque permission est représentée par un nombre :

- Lecture (r) est représentée par 4
- Écriture (w) est représentée par 2
- Exécution (x) est représentée par 1

Pour calculer la représentation octale, vous additionnez simplement les valeurs pour chaque permission. Par exemple :

- `rw-` (lecture et écriture) est 4 + 2 + 0 = 6
- `r--` (lecture seulement) est 4 + 0 + 0 = 4
- `rwx` (lecture, écriture et exécution) est 4 + 2 + 1 = 7

En utilisant la notation octale, les permissions pour les fichiers de notre exemple seraient :

```bash
644 file.txt
755 script.sh
```


### Mettre à jour les droits

#### chmod

Mettre à jour les permissions :

```bash
chmod [who][+|-|=][permissions] file
```

- `who` peut être `u` (user/propriétaire), `g` (groupe), ou `o` (autres).
- `+` ajoute les permissions spécifiées, tandis que `-` les supprime.
- `permissions` est la permission à ajouter ou supprimer (r, w, x).

Par exemple, pour ajouter la permission d'exécution pour l'utilisateur sur `script.sh`, vous lanceriez :

```bash
chmod u+x script.sh
chmod u+x,g-w script.sh # Assigner plusieurs permissions
chmod o=r-- script.sh
```

Pour changer les permissions en utilisant la notation octale :

```bash
chmod [permissions] file
```

Par exemple, pour définir les permissions de `file.txt` à `644`, vous lanceriez :

```bash
chmod 644 file.txt
```

#### Changer le propriétaire

La commande `chown` est utilisée pour changer le propriétaire et le groupe d'un fichier ou répertoire :

```bash
sudo chown [new_owner]:[new_group] file
```

Par exemple, pour changer le propriétaire de `file.txt` vers `alice` et le groupe vers `dev`, vous lanceriez :

```bash
sudo chown alice:dev file.txt
```

#### Changer le groupe

La commande `chgrp` est utilisée pour changer la propriété de groupe d'un fichier ou répertoire :

```bash
sudo chgrp [new_group] file
```

```bash
sudo chgrp dev file.txt
```

## Commandes utiles

### sudo

La commande `sudo` est utilisée pour exécuter une commande avec les privilèges de superutilisateur (root). C'est utile pour effectuer des tâches administratives qui nécessitent des permissions élevées. `sudo` est un groupe donc vous devez ajouter un nouvel utilisateur au groupe `sudo` pour lui accorder l'accès à cette commande.

```bash
sudo [command]
```

Par exemple, pour éditer un fichier système avec un éditeur de texte :

```bash
sudo nano /etc/hosts
```

### Mettre à jour un utilisateur

La commande `usermod` est utilisée pour modifier un compte utilisateur. Vous pouvez changer divers attributs de l'utilisateur, comme leur répertoire home, shell, ou appartenances aux groupes.

```bash
sudo usermod -d /new/home/dir alice  # Changer le répertoire home
sudo usermod -s /bin/zsh alice  # Changer le shell par défaut vers zsh
sudo usermod -L alice  # Verrouiller le compte utilisateur
sudo usermod -U alice  # Déverrouiller le compte utilisateur
```

### Vérifier le groupe utilisateur

```bash
id -ng

id -Gn # Lister tous les groupes dont l'utilisateur est membre
```
