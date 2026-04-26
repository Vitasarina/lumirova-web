# Lumírova — Live Preview

Astro dev server běžící v Dockeru, přístupný přes Tailscale na:

**http://100.117.196.90:4321**

## Jak to funguje

- Kontejner `web` (Astro dev server) startuje automaticky při restartu stroje (`restart: unless-stopped`).
- Cron každou minutu spustí `scripts/auto-pull.sh`:
  - `git pull --ff-only` — stáhne nové commity z main
  - Pokud přišly nové commity → `docker compose restart` — container se restartuje a načte změny
  - Pokud žádná změna → nic se neděje
- Po commitu do `main` se preview aktualizuje do ~2 minut.

## Správa

```bash
# Stav containeru
cd /home/agent/projects/lumirova-web
docker compose ps

# Logy
docker compose logs -f

# Ruční restart
docker compose restart

# Zastavení (bez automatického startu znovu)
docker compose stop

# Úplné vypnutí + smazání containeru
docker compose down

# Znovu spustit (pokud zastaveno)
docker compose up -d

# Logy auto-pull cronu
tail -f /tmp/lumirova-pull.log
```

## Rebuild po změně Dockerfile / závislostí

```bash
cd /home/agent/projects/lumirova-web
docker compose build && docker compose up -d
```
