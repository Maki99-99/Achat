# Achat — Projet DevOps

[![CI](https://github.com/Maki99-99/Achat/actions/workflows/ci.yml/badge.svg?branch=main)](https://github.com/Maki99-99/Achat/actions/workflows/ci.yml)

Application de gestion des achats développée avec Spring Boot dans le cadre du module DevOps. Le projet est organisé en branches Git par module fonctionnel, puis intégré dans la branche `main`.

## Fonctionnalités

| Module | Branche | Routes de base |
|---|---|---|
| Produits et catégories | `feature/produit` | `/produit`, `/categorieProduit` |
| Fournisseurs et secteurs d'activité | `feature/fournisseur` | `/fournisseur`, `/secteurActivite` |
| Factures et détails de facture | `feature/facture` | `/facture` |
| Règlements | `feature/reglement` | `/reglement` |
| Stock | `feature/stock` | `/stock` |
| Opérateurs | `feature/operateur` | `/operateur` |

## Stack technique

| Composant | Technologie |
|---|---|
| Langage | Java 8 |
| Framework | Spring Boot 2.5.3 (Web, Data JPA) |
| Build | Maven (wrapper inclus) |
| Base de données | MySQL / Hibernate |
| Documentation API | Springfox (Swagger) 3.0.0 |
| Boilerplate | Lombok |
| Tests | JUnit 5, H2 (en mémoire) |
| CI | GitHub Actions |

## Prérequis

- JDK 8
- MySQL 5.7 ou 8
- Aucune installation de Maven n'est nécessaire : le wrapper `./mvnw` est fourni.

## Configuration de la base de données

1. Créer la base :

```sql
CREATE DATABASE achatdb;
```

2. Renseigner les identifiants MySQL dans `src/main/resources/application.properties` :

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/achatdb?useUnicode=true&useJDBCCompliantTimezoneShift=true&useLegacyDatetimeCode=false&serverTimezone=UTC
spring.datasource.username=<utilisateur>
spring.datasource.password=<mot_de_passe>
```

Le schéma est mis à jour automatiquement au démarrage (`spring.jpa.hibernate.ddl-auto=update`).

## Lancer l'application

Linux / macOS :

```bash
./mvnw spring-boot:run
```

Windows :

```bash
mvnw.cmd spring-boot:run
```

Une fois démarrée :

- API : http://localhost:8089/SpringMVC
- Swagger UI : http://localhost:8089/SpringMVC/swagger-ui/
- Spécification OpenAPI : http://localhost:8089/SpringMVC/v3/api-docs

La configuration Swagger se trouve dans `src/main/java/tn/esprit/rh/achat/util/SpringFoxSwaggerConfig.java`.

## Tests

```bash
./mvnw test
```

Les tests utilisent une base H2 en mémoire (`src/test/resources/application.properties`) : aucune instance MySQL n'est nécessaire.

## Intégration continue

Le workflow [`.github/workflows/ci.yml`](.github/workflows/ci.yml) s'exécute :

- à chaque push sur `main` et sur les branches `feature/**` ;
- à chaque pull request vers `main`.

Il utilise Java 8 (Temurin), le cache Maven et lance `./mvnw -B clean verify`.

## Structure du projet

```
src/
├── main/
│   ├── java/tn/esprit/rh/achat/
│   │   ├── controllers/     # API REST
│   │   ├── entities/        # Entités JPA
│   │   ├── repositories/    # Repositories Spring Data
│   │   ├── services/        # Interfaces et implémentations
│   │   └── util/            # Configuration Swagger
│   └── resources/
│       └── application.properties
└── test/
    ├── java/tn/esprit/rh/achat/AchatApplicationTests.java
    └── resources/application.properties
```

## Organisation des branches

| Branche | Contenu |
|---|---|
| `main` | Version intégrée du projet (tous les modules, CI et tests) |
| `feature/produit` | Produits et catégories |
| `feature/fournisseur` | Fournisseurs et secteurs d'activité |
| `feature/facture` | Factures et détails de facture |
| `feature/reglement` | Règlements |
| `feature/stock` | Stock |
| `feature/operateur` | Opérateurs |
| `feature/github-actions` | Workflow GitHub Actions |
| `feature/tests-integration` | Tests d'intégration avec H2 |

Chaque branche de module ne contient que les classes de son module ; elle est ensuite fusionnée dans `main`.

## Auteur

**Maki99-99** — [github.com/Maki99-99](https://github.com/Maki99-99)

Dépôt : [github.com/Maki99-99/Achat](https://github.com/Maki99-99/Achat)
