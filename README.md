# PharmaFlow 💊

*Smart Pharmaceutical Supply Chain Management*

## 1. Présentation du projet

**PharmaFlow** est une plateforme de gestion de la chaîne d'approvisionnement pharmaceutique. Elle coordonne les offres des fournisseurs, les stocks des pharmacies, les commandes et les livraisons. Elle couvre aussi les campagnes de sensibilisation, les urgences d'approvisionnement ainsi que les réclamations et retours.

Les informations sur les offres, les stocks, les commandes et les réceptions sont aujourd'hui dispersées. PharmaFlow vise à :

- rendre les disponibilités visibles ;
- tracer les lots et suivre les péremptions ;
- coordonner les acteurs lorsqu'un besoin, normal ou urgent, apparaît ;
- alerter à partir des seuils de stock et des événements métier.

**Périmètre exclu :** paiement bancaire réel, prédiction par intelligence artificielle, triage médical et optimisation GPS avancée.

> **État du projet :** phase de conception (validation intermédiaire du module AWD, année universitaire 2026–2027). Les contrats REST, les événements et les règles décrits dans la documentation définissent le comportement attendu avant le développement métier ; ils ne constituent pas une preuve de réalisation ou de déploiement.

## 2. Architecture

PharmaFlow repose sur une architecture **microservices** : **8 services**, chacun avec sa **base de données indépendante**. Aucun service ne lit directement la base d'un autre ; les références externes sont des identifiants échangés par API ou par événements, sans clé étrangère entre bases.

- **Backend :** microservices Java / Spring Boot.
- **Frontend :** application Angular, qui accède aux API via la Gateway.
- **Communication :** REST avec OpenFeign pour les vérifications immédiates ; RabbitMQ pour les événements asynchrones.

### Les microservices

| # | Microservice | Responsabilité | Base de données |
|---|---|---|---|
| 1 | Supplier Service | Offres des fournisseurs, disponibilité commerciale et réservations | MySQL · `supplier_db` |
| 2 | Pharmacy Inventory Service | Pharmacies, référentiel des médicaments, stocks, lots, inventaires et péremptions | PostgreSQL · `inventory_db` |
| 3 | Order Service | Commandes des pharmacies, de la création à la clôture | MySQL · `order_db` |
| 4 | Delivery Service | Livraisons, livreurs, réceptions par lot, incidents | MongoDB · `delivery_db` |
| 5 | Campaign Service | Campagnes de sensibilisation, événements, inscriptions, évaluations | MongoDB · `campaign_db` |
| 6 | Emergency Service | Besoins urgents en médicaments et propositions de fournisseurs | PostgreSQL · `emergency_db` |
| 7 | Claims & Returns Service | Réclamations, décisions et retours fournisseur | PostgreSQL · `claims_db` |
| 8 | Notification Service | Confirmations, rappels et alertes (service commun à l'équipe) | MongoDB · `notification_db` |

### Composants d'infrastructure

| Composant | Rôle |
|---|---|
| Spring Cloud Gateway | Point d'entrée unique et routage |
| Eureka | Registre des instances (service discovery) |
| Spring Cloud Config | Configuration centralisée |
| Keycloak | Identités, OIDC / JWT et rôles |
| RabbitMQ | Échange d'événements entre services |
| Docker Compose | Exécution locale des conteneurs, réseaux et volumes |

### Rôles utilisateurs

- **Pharmacien** : consulter les stocks, commander, réceptionner, déclarer un besoin urgent ou une réclamation.
- **Fournisseur** : publier les offres, répondre aux urgences, confirmer ou refuser les commandes.
- **Livreur / responsable logistique** : organiser et exécuter les livraisons et les retours, tracer les incidents.
- **Administrateur** : gérer les droits et superviser les établissements.
- **Organisateur / participant** : gérer les événements de sensibilisation ; s'inscrire et évaluer sa participation.

### Parcours métier principaux

- **Réapprovisionnement :** commande → confirmation → expédition → réception → mise à jour du stock.
- **Urgence :** pénurie détectée → demande urgente → commande prioritaire.
- **Sensibilisation :** campagne → événement → inscriptions → participation.
- **Réclamation :** lot endommagé → réclamation → retour → avoir fournisseur.

## 3. Technologies utilisées

### Backend
- Java 17
- Spring Boot, Spring Web, Spring Data JPA, Spring Data MongoDB
- Spring Cloud (Gateway, Config, OpenFeign) et Eureka
- Spring Security (OAuth2 / JWT) avec Keycloak
- RabbitMQ
- MySQL, PostgreSQL, MongoDB
- Maven, Lombok, Jakarta Validation

### Frontend
- Angular
- TypeScript, HTML, CSS

### Outils et déploiement
- Docker et Docker Compose
- Git, GitHub et GitHub Projects
- IntelliJ IDEA, Visual Studio Code

## 4. Structure du dépôt

```text
PharmaFlow/
│
├── Backend/
│   ├── supplier-service/
│   ├── inventory-service/
│   ├── order-service/
│   ├── delivery-service/
│   ├── campaign-service/
│   ├── emergency-service/
│   ├── claims-service/
│   ├── notification-service/
│   └── infrastructure/        # gateway, eureka, config-server
│
├── Frontend/
│   └── pharmaflow-frontend/
│
├── Documentation/
│   ├── Presentation/
│   ├── Diagrams/
│   └── Technical-Report/
│
├── docker-compose.yml
├── README.md
└── .gitignore
```

## 5. Installation et exécution

### Prérequis

- Java JDK 17
- Maven
- Node.js et npm
- Angular CLI
- Docker et Docker Compose

### Lancer l'environnement avec Docker Compose

Le fichier `docker-compose.yml` décrit l'environnement prévu : Gateway, Eureka, Config Server, Keycloak, RabbitMQ, les huit services et leurs moteurs de bases de données.

```bash
docker compose up -d
```

Les secrets (mots de passe de bases, configuration Keycloak) sont fournis par variables d'environnement et ne sont **pas** versionnés.

### Lancer un microservice en local

Chaque microservice est un projet Spring Boot indépendant.

1. Accéder au dossier du microservice (par exemple `Backend/supplier-service`).
2. Vérifier que sa base de données, Eureka et le Config Server sont démarrés.
3. Lancer l'application :

```bash
mvn spring-boot:run
```

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

4. Ouvrir dans le navigateur : <http://localhost:4200>

## 6. Objectifs du projet

- Centraliser la gestion des pharmacies et des fournisseurs.
- Suivre les stocks, les lots et les péremptions.
- Simplifier la gestion des commandes et assurer le suivi des livraisons.
- Coordonner les urgences d'approvisionnement.
- Gérer les réclamations et les retours.
- Organiser des campagnes de sensibilisation.
- Améliorer la visibilité, la traçabilité et la coordination de la chaîne d'approvisionnement pharmaceutique.

## 7. Équipe et organisation

Projet réalisé dans le cadre du module **AWD** (année universitaire 2026–2027) par une équipe de 7 étudiants. Chaque membre est responsable d'un service métier ; le service Notification est réalisé en commun.

| Membre | Nom | Service |
|---|---|---|
| 1 | *à renseigner* | Supplier |
| 2 | *à renseigner* | Pharmacy Inventory |
| 3 | *à renseigner* | Order |
| 4 | *à renseigner* | Delivery |
| 5 | *à renseigner* | Campaign |
| 6 | *à renseigner* | Emergency |
| 7 | *à renseigner* | Claims & Returns |

**Encadrement :** *à renseigner*

**Dépôt GitHub :** *lien à renseigner*

---

*PharmaFlow – Smart Pharmaceutical Supply Chain Management*
