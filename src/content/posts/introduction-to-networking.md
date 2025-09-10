---
title: "Introduction aux réseaux"
published: 2025-09-04
draft: false
toc: true
description: "Apprenez les composants matériels fondamentaux et les protocoles qui alimentent la communication réseau, ainsi que les commandes Linux essentielles pour le dépannage réseau."
series: 'Basic'
tags: ['networking', 'tutorial']
---


## Modèle OSI
Le modèle OSI (Open Systems Interconnection) est un cadre conceptuel utilisé pour comprendre et implémenter les protocoles réseau en sept couches. Chaque couche remplit une fonction spécifique et communique avec les couches directement au-dessus et en-dessous d'elle.

1. **Couche physique** : Les fils et signaux réels
Exemple : Câble Ethernet transportant des signaux électriques, fibre optique, ondes radio Wi-Fi

2. **Couche liaison de données** : Communication appareil à appareil sur le même réseau
Exemple : Votre ordinateur portable parlant à votre routeur Wi-Fi, adresses MAC, commutateurs

3. **Couche réseau** : Trouver des chemins à travers différents réseaux
Exemple : GPS pour les données - routeur, NAT, adressage IP

4. **Couche transport** : Livraison fiable et vérification d'erreurs
Exemple : TCP s'assure que votre email arrive complet et dans l'ordre

5. **Couche session** : Gérer les conversations entre applications
Exemple : Maintenir votre appel vidéo connecté pendant 30 minutes

6. **Couche présentation** : Formatage des données et chiffrement
Exemple : Convertir les données HTTPS chiffrées en texte lisible

7. **Couche application** : Les programmes que vous utilisez réellement
Exemple : Votre navigateur web, client email, ou application de messagerie


## Composants matériels

### Commutateur
Entre le routeur et les ordinateurs, il y a un commutateur. Il connaît les adresses des appareils sur le réseau local (LAN). Il gère le trafic de données entre eux. Il fonctionne à la couche liaison de données (Couche 2) du modèle OSI.

### Routeur
Le routeur connecte le réseau local à internet. Il transfère les paquets de données entre différents réseaux. Il utilise une table de routage pour déterminer le meilleur chemin pour transférer les paquets. Il fonctionne à la couche réseau (Couche 3) du modèle OSI.

### Serveur DHCP
Le serveur DHCP (Dynamic Host Configuration Protocol) attribue des adresses IP aux appareils sur le réseau local. Il s'assure que chaque appareil a une adresse IP unique. Le serveur DHCP est souvent intégré dans le routeur. Il fonctionne à la couche application (Couche 7) du modèle OSI.

### Pare-feu
Un pare-feu surveille et contrôle le trafic réseau entrant et sortant basé sur des règles de sécurité prédéterminées. Il établit une barrière entre un réseau interne de confiance et des réseaux externes non fiables, comme internet. Les pare-feux peuvent être basés sur du matériel, des logiciels, ou une combinaison des deux.

## Protocoles

### Adresses IP
Une adresse IP (Internet Protocol address) est une étiquette numérique unique attribuée à chaque appareil connecté à un réseau. Elle remplit deux fonctions principales : identifier l'appareil et fournir l'emplacement de l'hôte dans le réseau. Il y a deux types d'adresses IP :

- IPv4 : 32-bit, 4 blocs (0-255) permettant environ 4,3 milliards d'adresses uniques (ex : 192.168.1.1).
- IPv6 : 128-bit, 8 blocs (0 - FFFF) permettant un nombre considérablement plus grand d'adresses uniques (ex : 2001:0db8:85a3:0000:0000:8a2e:0370:7334).

Masque : Un masque de sous-réseau est utilisé pour diviser une adresse IP en parties réseau et hôte. Il définit la frontière de votre réseau. Exemple :

```
255.255.255.0
 │   │   │   │
 │   │   │   └── Partie hôte (Entre 0 et 255)
 └───┴───┴────── Partie réseau (192.168.1 par exemple)
```

0.0.0.0/0 signifie "toutes les adresses IP". Les 4 premiers nombres sont l'adresse IP, le /0 est le masque.

255 dans cet exemple pourrait être 0, 128, 192, 224, 240, 248, 252, 254 ou 255. Si c'était 255, cela signifierait "tous les appareils dans ce réseau". Pour 128 ce serait "la première moitié des appareils dans ce réseau", par exemple :

Prend une IP comme 192.168.1.100 et dit "192.168.1 est votre quartier, 100 est votre numéro de maison."

La dernière adresse dans un sous-réseau est appelée l'adresse de diffusion. Elle est utilisée pour envoyer des données à tous les appareils du sous-réseau. Pour un sous-réseau avec un masque de 255.255.255.0, l'adresse de diffusion serait 192.168.1.255.

Trois notations :
- Binaire : 11111111.11111111.11111111.00000000
- Décimal : 255.255.255.0
- CIDR : /24

Exemple de calcul :
11111111.11111111.11111110.00000000

23 >> 1
9 >> 0

2^(32-23) - 2 = 510 - 2 = 508 hôtes

32 Longueur totale de l'adresse IP
-2 2 réservées (adresse réseau et diffusion)

128 - 64 - 32 - 16 - 8 - 4 - 2 - 1

#### Ports
Les ports sont comme des portes sur un ordinateur qui permettent à différents types de trafic réseau d'entrer et de sortir. Ils sont représentés par un nombre entre 0 et 65535. Certains ports sont réservés pour des services spécifiques :

- 80: HTTP (trafic web)
- 443: HTTPS (trafic web sécurisé)
- 22: SSH (shell sécurisé pour accès distant)
- 25: SMTP (envoi d'email)
- 53: DNS (système de noms de domaine)

Ils sont utilisés en plus des adresses IP pour diriger le trafic vers la bonne application ou service sur un appareil. Par exemple, quand vous visitez un site web, votre ordinateur se connecte à l'adresse IP du serveur sur le port 80 (HTTP), exemple : 75.2.70.75:80

### TCP
Un protocole de connexion qui assure une transmission fiable des données entre appareils. Il établit une connexion avant que les données soient envoyées et garantit que tous les paquets arrivent dans l'ordre et sans erreurs. Il est utilisé pour les applications où la fiabilité est cruciale, comme la navigation web (HTTP/HTTPS), l'email (SMTP), et les transferts de fichiers (FTP).

### UDP
Un protocole sans connexion qui ne garantit pas une transmission fiable des données. Il envoie des paquets sans établir de connexion et n'assure pas que les paquets arrivent dans l'ordre ou sans erreurs. Il est utilisé pour les applications où la vitesse est plus importante que la fiabilité, comme le streaming vidéo, les jeux en ligne, et la voix sur IP (VoIP).

### HTTP/HTTPS
HTTP (Hypertext Transfer Protocol) est la fondation de la communication de données sur le web. Il définit comment les messages sont formatés et transmis, et comment les serveurs web et navigateurs doivent répondre à diverses commandes.

### FTP
FTP (File Transfer Protocol) est un protocole réseau standard utilisé pour transférer des fichiers entre un client et un serveur sur un réseau basé TCP, comme internet. FTP fonctionne à la couche application (Couche 7) du modèle OSI.

### Adresse MAC
Une adresse MAC (Media Access Control) est un identifiant unique attribué à un contrôleur d'interface réseau (NIC) pour être utilisé comme adresse réseau dans les communications au sein d'un segment réseau. Les adresses MAC sont utilisées dans la couche liaison de données (Couche 2) du modèle OSI.

### ICMP
ICMP (Internet Control Message Protocol) est utilisé pour les messages d'erreur et l'information opérationnelle. Par exemple, la commande `ping` utilise ICMP pour tester l'accessibilité d'un hôte sur un réseau IP. Il fonctionne à la couche réseau (Couche 3) du modèle OSI.

### DORA
DORA signifie Discover, Offer, Request, Acknowledge (Découvrir, Offrir, Demander, Acquitter). C'est le processus utilisé par le DHCP (Dynamic Host Configuration Protocol) pour attribuer des adresses IP aux appareils sur un réseau.

## WAN et LAN
- WAN (Wide Area Network) : Un WAN est un réseau de télécommunications qui s'étend sur une grande zone géographique, souvent un pays ou un continent. Internet est le plus grand exemple de WAN.
- LAN (Local Area Network) : Un LAN est un réseau qui connecte ordinateurs et appareils dans une zone géographique limitée, comme une maison, école, ou bâtiment de bureau. Les LANs sont typiquement plus rapides et plus sécurisés que les WANs.

### NAT 
NAT consiste à traduire les IPs privées en IPs publiques pour que les appareils sur un réseau privé puissent accéder à internet.

- Plages d'IP privées (RFC1918) :
  - 10.0.0.0/8
  - 172.16.0.0/12
  - 192.168.0.0/16

- Comment NAT fonctionne :
  - Votre ordinateur portable a une IP privée, ex : 192.168.1.10.
  - Vous voulez atteindre 8.8.8.8 (DNS Google).
  - L'appareil NAT (habituellement un routeur) remplace votre IP privée par son IP publique pour les paquets sortants.
  - Quand les réponses reviennent, NAT le traduit de nouveau vers votre IP privée.

NAT est pourquoi plusieurs appareils dans votre maison peuvent partager une seule IP publique.


## Fichiers de configuration

### /etc/hosts
Le fichier `/etc/hosts` est un fichier texte simple qui mappe les noms d'hôtes aux adresses IP

networks
### /etc/resolv.conf
Le fichier `/etc/resolv.conf` est utilisé pour configurer les paramètres DNS (Domain Name System) sur un système Linux. Il spécifie les serveurs DNS que le système doit utiliser pour résoudre les noms de domaine en adresses IP.

### /etc/network/interfaces
Le fichier `/etc/network/interfaces` est utilisé pour configurer les interfaces réseau sur les distributions Linux basées Debian.

### /etc/hostname
Le fichier `/etc/hostname` contient le nom d'hôte du système. Le nom d'hôte est une étiquette lisible par l'homme qui est utilisée pour identifier le système sur un réseau.


## Commandes


### sudo /etc/init.d/networking restart
Redémarre le service réseau pour appliquer les changements faits aux fichiers de configuration réseau.

### ping
La commande `ping` est utilisée pour tester l'accessibilité d'un hôte sur un réseau IP. 

```bash
ping 8.8.8.8  # Ping du serveur DNS public de Google
ping example.com  # Ping d'un nom de domaine
```

### ip
La commande `ip` est utilisée pour afficher et manipuler le routage, les appareils, le routage de politique, et les tunnels.

```bash
ip addr show          # Afficher toutes les adresses IP
ip link show          # Afficher toutes les interfaces réseau
ip route show         # Afficher la table de routage  
```

### traceroute
La commande `traceroute` est utilisée pour tracer le chemin que prennent les paquets de votre ordinateur vers un hôte de destination.

```bash
traceroute example.com  # Tracer la route vers example.com
```

### dhclient
La commande `dhclient` est un client DHCP qui est utilisé pour obtenir une adresse IP et d'autres paramètres de configuration réseau d'un serveur DHCP.

```bash
sudo dhclient -v # Demander une adresse IP avec sortie détaillée
```

### nmap
La commande `nmap` est un outil de scan réseau utilisé pour découvrir des hôtes et services sur un réseau informatique.

```bash
nmap google.com # Scanner google.com pour les ports ouverts 
```
