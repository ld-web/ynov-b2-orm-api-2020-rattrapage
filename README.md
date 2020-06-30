# ORM / API - Ynov B2 - Rattrapage

Vous allez réaliser une API crowdfunding.

Critères d'évaluation :

- Organisation et séparation du code
- Création et configuration d'une API avec API Platform
- Application de filtres
- Utilisation des groupes de sérialisation
- Relations entre entités
- DTO

## Mode de rendu

Lien vers votre dépôt Git, que je pourrai clôner.

## Dépôt Git

Votre dépôt Git contiendra un fichier `README.md` dans lequel vous indiquerez :

- Qu'est-ce qu'un DTO et à quoi sert-il ?
- Quelle est la différence entre un listener et un subscriber dans Symfony ?
- Qu'est-ce qu'un JWT ? Pourquoi l'utilise-t-on plutôt que les sessions PHP ?
- Qu'est-ce que CORS ?
- Quelle est la différence entre JSON et JSON-LD ?

## Exercice

Votre API permettra de recevoir des paiements fictifs destinés à des projets de crowdfunding enregistrés dans votre base de données.

> Aucune authentification ne sera demandée (donc pas de JWT) dans le cadre de cet exercice. Vous n'avez donc pas à créer d'entité `Utilisateur`, ni d'entité `Auteur` par exemple

### Structure de la base de données

> Entité : Project

| Champ | Type | Commentaires |
|---|---|---|
| id | integer | Clé primaire |
| name | string | |
| startDate | date | Date de démarrage du projet |
| endDate | date | Date de fin du projet, après laquelle plus aucun paiement ne sera possible |
| picture | string | Image d'illustration du projet |
| description | text | Description du projet |
| goal | integer | Montant final visé (en Euros €) |
| payments | **Relation** | Paiements enregistrés pour ce projet |
| created | date | Date de création de l'enregistrement, renseignée automatiquement à la création de l'enregistrement |

> Entité : Payment

| Champ | Type | Commentaires |
|---|---|---|
| id | integer | Clé primaire |
| donator_name | string | Nom renseigné par le donateur au moment du paiement |
| amount | integer | Montant du paiement |
| comment | string | Un court commentaire éventuellement laissé par le donateur |
| payment_date | date | Date de paiement enregistrée |
| project | **Relation** | Projet financé par le paiement |
| created | date | Date de création de l'enregistrement, renseignée automatiquement à la création de l'enregistrement |

### Fixtures

Vous réaliserez des fixtures pour chaque entité, afin d'avoir un jeu de données initial.

## Fonctionnalités

> Toutes les entités seront des ressources de l'API présentant un CRUD complet.

### Formats

Les formats activés seront JSON-LD, JSON et CSV.

### Contrôle d'accès

Vous pouvez laisser l'API en publique, ce qui nous intéresse ici est plus API Platform, l'organisation de votre code, les groupes de sérialisation et vos DTO, que l'authentification.

### Recherche

L'API donnera la possibilité de rechercher un projet par nom (stratégie : nom partiel, insensible à la casse).

### Sérialisation et DTO

Project :

- name
- startDate
- endDate
- picture
- description
- goal
- nbPayments
- currentTotalAmount
- payments
  - payment_date
  - donator_name
  - amount
  - comment

>`nbPayments` représente le nombre de paiements enregistrés pour ce projet
>
>`currentTotalAmount` représente le total en Euros (€) de tous les paiements enregistrés pour ce projet. Par défaut, sera à 0 si aucun paiement n'a été enregistré

Payment :

- payment_date
- donator_name
- amount
- comment
- project
  - name
  - startDate
  - endDate
