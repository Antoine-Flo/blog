---
title: "Cryptographie"
published: 2025-09-04
draft: false
toc: true
description: "Apprenez les bases de la cryptographie et comment l'utiliser pour sécuriser vos communications."
series: 'Basic'
tags: ['networking', 'tutorial']
---

## Clé SSH
Pour vous connecter en toute sécurité à un serveur distant, vous pouvez utiliser SSH (Secure Shell). La méthode la plus sûre pour s'authentifier est d'utiliser une paire de clés SSH : une clé publique et une clé privée.


```bash
ssh-keygen -t ed25519 -C "your_email@example.com" # ed25519 is the algorithm used to generate the key

# If you are using an older system that doesn't support Ed25519
ssh-keygen -t rsa -b 4096
```

Vous pouvez ajouter votre clé publique au serveur distant en le collant dans le fichier `~/.ssh/authorized_keys` ou en utilisant la commande `ssh-copy-id` :

```bash
ssh-copy-id -i ~/.ssh/id_ed25519.pub user@hostname_or_ip
```

Vous pouvez utiliser un agent SSH pour gérer vos clés privées. Voici comment démarrer l'agent SSH et ajouter votre clé privée :

```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_rsa
```

Pour voir toutes les clés actuellement gérées par l'agent SSH, utilisez :

```bash
ssh-add -l
```

Sur votre serveur distant, assurez-vous que le fichier `~/.ssh/authorized_keys` contient votre clé publique.

> Vous pouvez également utiliser un gestionnaire de clés comme [sshs](https://github.com/quantumsheep/sshs) pour simplifier la gestion des clés SSH.

Pour vous connecter à votre serveur distant, utilisez la commande suivante :

```bash
ssh user@hostname_or_ip
```


### Clé publique
Une clé publique est un fichier que vous pouvez partager avec n'importe qui. Elle est utilisée pour chiffrer les données qui ne peuvent être déchiffrées qu'avec la clé privée correspondante.

Exemple de clé publique (id_rsa.pub) :

```txt
ssh-rsa AAAAB3NzaC1yc2EAAAABIwAAAQEAr... user@hostname
```

### Clé privée
Une clé privée est un fichier sécurisé que vous gardez secret. Elle est utilisée pour prouver votre identité lorsque vous vous connectez à un serveur. Ne partagez jamais votre clé privée avec qui que ce soit.

Exemple de clé privée (id_rsa) :

```txt
-----BEGIN RSA PRIVATE KEY-----
MIIEpAIBAAKCAQEA7n...
-----END RSA PRIVATE KEY-----
```
