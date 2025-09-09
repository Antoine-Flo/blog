---
title: "Les commandes Linux essentielles"
published: 2025-09-01
draft: false
toc: true
description: "Une compilation des commandes Linux les plus importantes, de la gestion de fichiers au contrôle des processus."
series: 'Linux'
tags: ['cli', 'bash']
---

Toutes ces commandes fonctionnent en bash et devraient couvrir la majorité de vos besoins. Elles sont installées par défaut dans la plupart des distributions Linux.

## Documentation
Obtenez les connaissances directement depuis la ligne de commande.

### man
La seule commande nécessaire pour comprendre toute les autres. Affiche les options, les modèles d'utilisation et les exemples.

```bash
man mv

man -k search_term  # rechercher des commandes contenant le mot-clé
```

### -h ou --help
La plupart des commandes supportent l'option -h ou --help pour afficher une aide rapide.

```bash
mv --help
```

## Se déplacer
Apprenez à naviguer dans le système de fichiers.

### pwd
Affiche le chemin du dossier dans lequel vous vous trouvez.

```bash
pwd                  # Sortie : /home/username/documents
```

### cd
Se déplacer entre les répertoires. Naviguez dans le système de fichiers en changeant votre emplacement actuel. Dans les versions récentes de bash, vous n'avez même pas besoin d'utiliser CD, vous pouvez simplement taper le nom du répertoire.

```bash
cd /home/user        # aller vers un chemin spécifique
cd ..                # remonter d'un niveau
cd ~                 # aller au répertoire home
cd -                 # retourner au répertoire précédent
cd                   # aller au répertoire home (raccourci)

my_folder            # aller vers my_folder
```

### ls
Lister les fichiers et dossiers dans le répertoire actuel. Montre ce qui est disponible à votre emplacement actuel.

```bash
ls                     # listage basique
ls -l                  # liste détaillée avec permissions, taille, date
ls -la                 # inclure les fichiers cachés (commençant par .)
ls -lh                 # tailles de fichiers lisibles par l'humain
ls *.txt               # lister tous les fichiers avec l'extension .txt
```

## Manipuler les fichiers et dossiers

### touch
Créer un fichier vide ou mettre à jour l'horodatage d'un fichier existant. Moyen rapide de créer de nouveaux fichiers.

```bash
touch newfile.txt
touch file1.txt file2.txt file3.txt
```

### mkdir
Créer de nouveaux répertoires. Construire une structure de dossiers pour organiser les fichiers.

```bash
mkdir newfolder
mkdir folder1 folder2 folder3
mkdir -p path/to/deep/folder       # utiliser -p aussi pour éviter les erreurs si le dossier existe
mkdir -p project/{src,docs,tests}
```

### mv
Déplacer des fichiers/dossiers vers un nouvel emplacement ou les renommer.

```bash
mv oldname.txt newname.txt           # renommer un fichier
mv file.txt /path/to/destination/    # déplacer un fichier vers un autre répertoire
mv folder/ /new/location/            # déplacer un dossier entier
mv *.txt documents/                  # déplacer tous les fichiers .txt vers le dossier documents
```

### rm
Supprimer définitivement des fichiers et répertoires. Attention - il n'y a pas de corbeille dans le terminal.

```bash
rm file.txt                          # supprimer un seul fichier
rm file1.txt file2.txt               # supprimer plusieurs fichiers
rm -r folder/                        # supprimer un dossier et tout son contenu récursivement
rm -rf dangerous_folder/             # forcer la suppression sans confirmation
rm *.tmp                               # supprimer tous les fichiers .tmp
```

## Manipuler le texte

### echo
Afficher du texte dans la sortie du terminal. Afficher des messages, des variables, ou créer du contenu textuel simple.

```bash
echo "Hi mom !"                      # afficher du texte simple
echo "Hello $USER"                   # afficher avec une variable
echo -n "No newline"                 # afficher sans nouvelle ligne à la fin
echo "Line 1\nLine 2"                # afficher avec des caractères de nouvelle ligne

```

### cat
Afficher tout le contenu de fichier(s) dans le terminal. Voir le contenu des fichiers ou combiner plusieurs fichiers.

```bash
cat file.txt                         # afficher le contenu du fichier
cat file1.txt file2.txt              # afficher plusieurs fichiers
cat -n file.txt                      # afficher avec numéros de ligne
cat > newfile.txt                    # créer un fichier et taper le contenu (Ctrl+D pour sauvegarder)
```

### cut
Extraire des colonnes ou champs spécifiques du texte. Utile pour traiter des données structurées comme les fichiers CSV.

```bash
cut -d',' -f2 data.csv               # extraire la 2ème colonne du CSV
cut -d':' -f1,3 /etc/passwd          # extraire les 1er et 3ème champs
cut -c1-5 file.txt                   # extraire les caractères 1-5 de chaque ligne
echo "a,b,c,d" | cut -d',' -f2-4        # extraire les colonnes 2 à 4
```

### sort
Trier les lignes de texte par ordre alphabétique ou numérique. Organiser les données dans un ordre lisible.

```bash
sort file.txt                        # tri alphabétique
sort -n numbers.txt                  # tri numérique
sort -r file.txt                     # tri inversé
sort -u file.txt                     # trier et supprimer les doublons
sort -k2 data.txt                    # trier par la 2ème colonne
```

### tr
Remplacer ou transformer des caractères dans un flux de texte. Modifier le texte en substituant des caractères.

```bash
echo "hello" | tr 'l' 'x'            # remplacer 'l' par 'x'
echo "HELLO" | tr 'A-Z' 'a-z'        # convertir en minuscules
echo "hello world" | tr ' ' '_'      # remplacer les espaces par des traits de soulignement
echo "abc123" | tr -d '0-9'             # supprimer tous les chiffres
```

### wc
Compter les lignes, mots et caractères dans les fichiers. Obtenir des statistiques sur le contenu textuel.

```bash
wc file.txt                          # afficher lignes, mots, caractères
wc -l file.txt                       # compter seulement les lignes
wc -w file.txt                       # compter seulement les mots
wc -c file.txt                       # compter seulement les caractères
echo "hello world" | wc -w           # compter les mots dans une chaîne
```

### awk
Effectuer la manipulation de texte et l'extraction de données. Pratique quand le texte ressemble à un tableau.

```bash
awk '{print $1}' file.txt                   # afficher la première colonne
awk '{print $NF}' file.txt                  # afficher la dernière colonne
awk '{sum += $3} END {print sum}' file.txt  # additionner toutes les valeurs de la colonne 3

# Calculer la moyenne des nombres de la deuxième colonne
awk '{sum += $2; count++} END {print sum/count}' numbers.txt

# Afficher les lignes de plus de 80 caractères
awk 'length > 80' file.txt
```

### sed
Similaire à awk, plus adapté aux remplacements complexes basés sur les regex.

```bash
sed 's/old/new/g' file.txt   # remplacer toutes les occurrences d'"old" par "new"
sed '/pattern/d' file.txt    # supprimer les lignes correspondant au motif
sed 's/^#.*$//' file.txt     # supprimer les commentaires des scripts shell
sed '1,3d' file.txt          # supprimer les lignes 1 à 3
sed 's/ /\n/g' file.txt      # remplacer les espaces par des nouvelles lignes
```

## Commandes système

### whoami
Afficher le nom de l'utilisateur actuel. Identifier le compte utilisateur que vous utilisez actuellement.

```bash
whoami                               # affiche le nom d'utilisateur actuel
```

### systemctl
Contrôler et gérer les services système. Démarrer, arrêter, activer ou vérifier le statut des services.

```bash
systemctl status nginx                # vérifier le statut du service nginx
systemctl start nginx                 # démarrer le service nginx
systemctl stop nginx                  # arrêter le service nginx
systemctl restart nginx               # redémarrer le service nginx
systemctl enable nginx                # activer nginx pour démarrer au boot
systemctl disable nginx               # désactiver nginx du démarrage au boot
```

### ps aux
Afficher les processus en cours d'exécution avec des informations détaillées. Surveiller ce qui s'exécute sur votre système.


```bash
ps aux                              # afficher tous les processus
ps aux | grep firefox               # trouver un processus spécifique
ps -ef                              # format alternatif
ps -u username                      # afficher les processus pour un utilisateur spécifique
```

### kill

Arrêter un processus en cours d'exécution en envoyant des signaux de terminaison. Terminer des programmes qui ne répondent pas ou indésirables.

```bash
kill 1234                           # terminer le processus avec l'ID 1234
kill -9 1234                        # forcer l'arrêt (SIGKILL)
kill -15 1234                       # terminaison gracieuse (SIGTERM)
killall firefox                     # tuer tous les processus firefox
```

### df
Afficher l'utilisation de l'espace disque pour les systèmes de fichiers montés. Surveiller l'espace de stockage disponible.

```bash
df                                   # afficher l'utilisation du disque
df -h                                # tailles lisibles par l'humain (GB, MB)
df -h /home                          # vérifier un répertoire spécifique
df -i                                # afficher l'utilisation des inodes
```

### printenv
Afficher une ou toutes les variables d'environnement. Utile pour le débogage et la vérification de la configuration.

```bash
printenv HOME
printenv
```

### history
Vérifier les commandes précédemment exécutées. Examiner et réutiliser votre historique de commandes.

```bash
history                              # afficher tout l'historique des commandes
history | tail -10                   # afficher les 10 dernières commandes
history | grep "git"                 # rechercher les commandes git dans l'historique
!123                                 # ré-exécuter la commande numéro 123
!!                                   # ré-exécuter la dernière commande
```

### ip a
Trouver les informations d'interface réseau incluant les adresses IP. Vérifier votre configuration réseau.

```bash
ip a                                 # afficher toutes les interfaces réseau
ip addr show                         # syntaxe alternative
ip a show eth0                       # afficher une interface spécifique
ip route                             # afficher la table de routage
```


### curl
Effectuer des requêtes HTTP vers des serveurs web. Télécharger du contenu, tester des API, ou vérifier le statut de sites web.

```bash
curl www.google.com                            # obtenir le contenu d'une page web
curl -I www.google.com                         # obtenir seulement les en-têtes
curl -o page.html www.example.com              # sauvegarder la réponse dans un fichier
curl -X POST -d "data=value" api.com           # envoyer une requête POST avec des données
curl -s https://api.github.com/users/octocat   # mode silencieux (pas de progression)

```

## Redirections

### >
Envoyer la sortie d'une commande vers un fichier, en remplaçant le contenu existant. Rediriger la sortie pour créer ou écraser des fichiers.

```bash
echo "Hello" > file.txt              # créer un fichier avec du contenu
ls > filelist.txt                    # sauvegarder le listage du répertoire dans un fichier
cat file1.txt > copy.txt             # copier le contenu d'un fichier vers un nouveau fichier
date > timestamp.txt                 # sauvegarder la date actuelle dans un fichier
```

### >>
Envoyer la sortie d'une commande vers un fichier, en ajoutant au contenu existant. Ajouter la sortie à la fin des fichiers existants.

```bash
echo "New line" >> file.txt          # ajouter une ligne au fichier existant
ls >> filelist.txt                   # ajouter le listage du répertoire
cat file2.txt >> combined.txt        # ajouter le contenu du fichier
date >> log.txt                      # ajouter l'horodatage au journal
```

### |
Envoyer la sortie d'une commande comme entrée de la commande suivante. Enchaîner les commandes pour des opérations complexes.

```bash
cat logs.txt | wc -l                 # compter les lignes dans le fichier
ls -la | grep "txt"                  # lister seulement les fichiers .txt
ps aux | grep firefox                # trouver les processus firefox
cat data.csv | cut -d',' -f2 | sort  # extraire une colonne, puis trier
```

### xargs
Passer la sortie comme arguments à une autre commande. Convertir l'entrée en arguments de commande.

```bash
find . -name "*.txt" | xargs rm         # trouver et supprimer tous les fichiers .txt
echo "file1 file2 file3" | xargs touch  # créer plusieurs fichiers
ls *.txt | xargs -I {} cp {} backup/    # copier chaque fichier vers le dossier de sauvegarde
cat filelist.txt | xargs grep "error"   # rechercher "error" dans les fichiers listés
```

## Caractères génériques
### *
Correspondre à zéro ou plusieurs caractères. Sélectionner plusieurs fichiers avec la correspondance de motifs.

```bash
ls *.txt                             # lister tous les fichiers .txt
rm temp*                             # supprimer les fichiers commençant par "temp"
cp /path/*.jpg images/               # copier tous les fichiers jpg
echo file*.log                       # étendre aux noms de fichiers correspondants
```

### ?
Correspondre exactement à un caractère. Correspondance précise de motif à caractère unique.
```bash
ls file?.txt                         # correspondre à file1.txt, fileA.txt, etc.
rm temp?.log                         # supprimer temp1.log, tempX.log, etc.
cp image?.png backup/                # copier image1.png, imageA.png, etc.
```

### [1-2]
Correspondre à n'importe quel caractère dans la plage ou l'ensemble spécifié. Définir des alternatives de caractères spécifiques.

```bash
ls file[1-5].txt                     # correspondre à file1.txt jusqu'à file5.txt
rm log[ABC].txt                      # supprimer logA.txt, logB.txt, logC.txt
cp data[0-9][0-9].csv archive/       # correspondre à data01.csv, data99.csv, etc.
ls [a-z]*.txt                        # fichiers commençant par une lettre minuscule
```

## Utilitaires

### apt
Pour installer des paquets sur les systèmes basés sur Debian.

```bash
sudo apt update                # mettre à jour la liste des paquets
sudo apt install package_name  # installer un paquet
sudo apt remove package_name   # supprimer un paquet
```

### crontab
Programmer des tâches récurrentes avec cron.

```bash
crontab -e                            # éditer le crontab
crontab -l                            # lister les tâches cron actuelles
crontab -r                            # supprimer toutes les tâches cron
```

### date
Afficher la date et l'heure actuelles.

```bash
date               # mar. 02 sept. 2025 15:44:52 CEST
date -u            # mar. 02 sept. 2025 13:44:52 UTC
date +"%Y-%m-%d"   # 2025-09-02
```

### free
Afficher des informations sur l'utilisation de la mémoire système.

```bash
free               # afficher l'utilisation de la mémoire
free -h            # afficher l'utilisation de la mémoire dans un format lisible par l'humain
```

### du
Vérifier la taille d'un dossier

```bash
du -sh /folder
```

### dig
Effectuer des requêtes DNS pour obtenir des informations sur les domaines.

```bash
dig example.com              # obtenir les enregistrements A
dig example.com MX           # obtenir les enregistrements MX
dig example.com ANY          # obtenir tous les enregistrements
```

## Manipulation de chemins

### basename
Obtenir le nom de fichier à partir d'un chemin complet.

```bash
basename /path/to/file.txt         # Sortie: file.txt
basename /path/to/file.txt .txt    # Sortie: file
```

### realpath
Obtenir le chemin absolu d'un fichier ou répertoire.

```bash
realpath file.txt                   # Sortie: /full/path/to/file.txt
realpath ../relative/path           # Sortie: /full/path/to/relative/path
```