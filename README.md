﻿# Groupomania - Réseau social d'entreprise

7ème projet de la formation de [développeur web de OpenClassrooms]

## Scénario

Développement (Frontend et Backend) d'un réseau social d'entreprise pour une société fictive Groupomania.  
Une grande liberté est donnée pour développer ce projet: il faut simplement respecter la charte graphique fournie.

## Outils utilisés

Frontend : Boostrap, Vue
Backend : MySQL, Sequelize, NodeJS

## Lancement du projet

Pour accéder à toute les fonctionnalités disponibles du projet Groupomania vous devez :

### 1. Lancer le backend

Aller dans le répertoire backend et effectuer dans le terminal:
-> npm install
-> créer un dossier images à la racine du dossier backend
-> créer un dossier .env à la racine du dossier backend avec ces valeurs

DB_HOST= 127.0.0.1
DB_USERNAME= "root"
DB_PASSWORD= "sagat9011"
DB_NAME= database_development_groupomania
DB_NAME_TEST= database_test_groupomania
DB_NAME_PROD= database_production_groupomania
TOKENSECRET = WyjzFWUpsd

-> nodemon serve

Installer MySQL
Installer un serveur de base de donnée comme MAMP ou XAMPP

Utiliser le terminal MySQL pour créer 3 bases de données
database_development_groupomania / database_test_groupomania / database_production_groupomania

Utiliser de nouveau le terminal du situé dans le backend et effectuer:
-> sequelize db:create
-> sequelize db:migrate

### 2. Lancer le frontend

Aller dans le répertoire frontend et effectuer dans le terminal:
-> npm install
-> npm install -g @vue/cli
-> npm run serve

(Si vous n'utilisez pas npm, utilisez yarn)

### Crédit

Duplay Benjamin
benduplay@gmail.com
