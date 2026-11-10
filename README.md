# PharmaFlow 💊

## 1. Présentation du projet

**PharmaFlow** est une application intelligente de gestion de la chaîne d'approvisionnement pharmaceutique.

Elle a pour objectif de faciliter la gestion des pharmacies, des fournisseurs, des stocks, des commandes et des livraisons grâce à une architecture basée sur les microservices.

Le projet intègre également un service de prédiction utilisant l'intelligence artificielle afin d'améliorer la gestion des stocks et d'anticiper les besoins.

## 2. Architecture du projet

PharmaFlow adopte une architecture **Microservices**. Chaque service est indépendant et possède une responsabilité spécifique.

Le projet est organisé en deux parties principales :

- **Backend :** ensemble des microservices développés avec Spring Boot.
- **Frontend :** interface utilisateur développée avec Angular.

### Les microservices Backend

| Microservice | Responsabilité |
|---|---|
| Supplier Service | Gestion des fournisseurs |
| Inventory Service | Gestion des stocks et des produits |
| Order Service | Gestion des commandes |
| Delivery Service | Gestion des livraisons |
| AI Prediction Service | Prédiction des besoins et des stocks |
| Pharmacy Management Service | Gestion des pharmacies |

## 3. Technologies utilisées

### Backend
- Java 17
- Spring Boot
- Spring Data JPA
- Spring Web
- MySQL
- Maven
- Lombok
- Jakarta Validation

### Frontend
- Angular
- TypeScript
- HTML
- CSS

### Outils
- IntelliJ IDEA
- Visual Studio Code
- Git et GitHub
- XAMPP

## 4. Structure du dépôt

```text
PharmaFlow/
│
├── Backend/
│   ├── supplier-service/
│   ├── inventory-service/
│   ├── order-service/
│   ├── delivery-service/
│   ├── ai-prediction-service/
│   └── pharmacy-service/
│
├── Frontend/
│   └── pharmaflow-frontend/
│
├── README.md
└── .gitignore
```

## 5. Installation et exécution

### Prérequis

Avant de lancer le projet, installer :

- Java JDK 17
- Maven
- Node.js et npm
- Angular CLI
- MySQL

### Lancer le Backend

Chaque microservice est un projet Spring Boot indépendant.

1. Accéder au dossier du microservice souhaité.
2. Configurer la connexion à la base de données dans `application.properties`.
3. Vérifier que MySQL est démarré.
4. Lancer l'application Spring Boot.

### Lancer le Frontend

1. Accéder au dossier `Frontend/pharmaflow-frontend`.
2. Installer les dépendances :

```bash
npm install
```

3. Démarrer l'application Angular :

```bash
ng serve
```

4. Ouvrir dans le navigateur :

```text
http://localhost:4200
```

## 6. Objectifs du projet

- Centraliser la gestion des pharmacies et des fournisseurs.
- Faciliter le suivi des stocks.
- Simplifier la gestion des commandes.
- Assurer le suivi des livraisons.
- Exploiter l'intelligence artificielle pour anticiper les besoins.
- Améliorer l'efficacité de la chaîne d'approvisionnement pharmaceutique.

## 7. Auteurs

Projet réalisé dans le cadre d'un projet académique.

**Nom du projet :** PharmaFlow

**Dépôt GitHub :** [PharmaFlow](https://github.com/)

---

*PharmaFlow – Smart Pharmaceutical Supply Chain Management*
