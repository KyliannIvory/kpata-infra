# kpata-infra

Infrastructure de déploiement de l'application Kpata (frontend + backend), basée sur Docker Compose et Nginx en reverse proxy avec support HTTPS.

## Stack

- **Nginx** — reverse proxy, terminaison SSL
- **Frontend** — image `ghcr.io/kyliannivory/kpata-frontend`
- **Backend** — image `ghcr.io/kyliannivory/kpata-backend`
- **PostgreSQL 16** — base de données

## Prérequis

- Docker et Docker Compose
- Un réseau Docker externe nommé `kpata_network` :
  ```
  docker network create kpata_network
  ```
- Des certificats SSL dans `nginx/certs/` (`kpata.local.crt` et `kpata.local.key`)

## Configuration

Copier `.env.example` vers `.env` et renseigner les valeurs (mot de passe DB, secret JWT, etc.) :

```
cp .env.example .env
```

## Lancer en local

```
docker compose up -d
```

## Déploiement continu (CD)

Un workflow GitHub Actions (`.github/workflows/cd.yml`) est en place pour automatiser le déploiement sur un serveur cible. Il est déclenché manuellement (`workflow_dispatch`) et s'appuie sur un runner **self-hosted**.

⚠️ Ce runner n'est pas encore configuré : le workflow ne peut pas s'exécuter tant qu'aucun serveur (VPS) n'est enregistré comme runner self-hosted GitHub Actions.
