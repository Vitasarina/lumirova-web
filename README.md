# SVJ Lumírova 8, 10 – web

Statický web SVJ Lumírova 8, 10 (Ostrava). Stack: **Astro** + **Tailwind CSS**.

## Rychlý start (lokální vývoj s Dockerem)

### Požadavky

- [Docker](https://docs.docker.com/get-docker/) + Docker Compose v2

### Spuštění

```bash
# Naklonuj repozitář
git clone https://github.com/Vitasarina/lumirova-web.git
cd lumirova-web

# Spusť dev server
docker compose up
```

Astro dev server běží na **http://localhost:4321** s live hot-reload.

### Zastavení

```bash
docker compose down
```

### Smazání volumes (node_modules cache)

```bash
docker compose down -v
```

## Lokální vývoj bez Dockeru

```bash
npm install
npm run dev
# http://localhost:4321
```

## Struktura

```
lumirova-web/
├── docker/                  # Docker infrastruktura
│   ├── Dockerfile
│   └── docker-compose.yml
├── src/
│   └── pages/
│       └── index.astro
├── public/
├── .github/workflows/
│   └── deploy.yml           # GH Actions skeleton (CF Pages – TODO)
├── astro.config.mjs
├── tailwind.config.mjs
├── docker-compose.yml       # Include shortcut → docker/docker-compose.yml
└── package.json
```

## Deploy

Deploy na Cloudflare Pages je připraven jako skeleton v `.github/workflows/deploy.yml`.
Je spouštěn ručně (`workflow_dispatch`) — automatický deploy bude aktivován po konfiguraci CF Pages projektu a nastavení secrets `CF_API_TOKEN` a `CF_ACCOUNT_ID`.
