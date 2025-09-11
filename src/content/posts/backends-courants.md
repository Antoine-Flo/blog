---
title: "Déployer différents backends"
published: 2025-09-11
draft: false
toc: true
description: "Des exemples de frameworks backend dans plusieurs langages. Leurs fichiers de configurations, et comment les déployer."
series: 'Code'
tags: ['backend', 'bash']
---

Les différentes commandes à réaliser pour déployer des backends dans plusieurs langages et frameworks populaires.

## Node.js
Node.js utilise un fichier `package.json` pour gérer les dépendances et les scripts.

### Express / NestJS
```bash
npm install
npm start
```

## Python
Python utilise des environnements virtuels et des fichiers `requirements.txt` pour gérer les dépendances. Python utilise un environnement virtuel pour isoler les dépendances.

```bash
python -m venv venv
deactivate                # Pour désactiver l'environnement virtuel
source venv/bin/activate  # Pour reactiver l'environnement virtuel
```

### Flask
```bash
pip install -r requirements.txt
python app.py
```

### Django
```bash
pip install -r requirements.txt
python manage.py runserver
```

## Java
Java utilise des outils comme Maven (pom.xml) ou Gradle (build.gradle) pour gérer les dépendances et les builds.

### Spring Boot
```bash
mvn clean install
java -jar target/myapp.jar
mvn spring-boot:run
```

## Php
PHP utilise des gestionnaires de dépendances comme Composer (composer.json).

### Laravel
```bash
composer install
php artisan serve
```

### Symfony
```bash
composer install
php bin/console server:run
```

## C#
C# utilise .NET CLI pour gérer les projets et les dépendances. Deux fichiers sont couramment utilisés : `.csproj` et `global.json`. Ils permettent de définir les configurations du projet et les versions du SDK .NET à utiliser.

### .NET Core
```bash
dotnet restore
dotnet run
```

## Go
Go utilise des modules (go.mod) pour gérer les dépendances.

### Gin
```bash
go mod tidy
go run main.go        # Pour le développement

go build -o myapp     # Pour la production
./myapp
```

## Rust
Rust utilise Cargo (Cargo.toml) pour gérer les dépendances et les builds.

### Actix
```bash
cargo build
cargo run
```