# Immich Homelab

Self-hosted Immich deployment managed with Docker Compose + Coolify.

## Architecture

```text
Host
  ├── Docker
  ├── Coolify
  ├── Cloudflare Tunnel
  └── Mount Management

Coolify
  ├── Immich Deployment
  ├── Environment Variables
  ├── Logs
  └── Scheduled Jobs

Storage
  ├── /mnt/storage
  └── /mnt/storage-backup
```

---

# Directory Structure

```text
/opt/
└── immich/
    ├── docker-compose.yml
    ├── .env
    └── README.md

/mnt/
├── storage/
│   └── immich/
│       ├── backups/
│       ├── encoded-video/
│       ├── library/
│       ├── profile/
│       ├── thumbs/
│       └── upload/
│
└── storage-backup/
    └── mirror of /mnt/storage
```

---

# Environment Variables

```env
UPLOAD_LOCATION=/mnt/storage/immich
DB_DATA_LOCATION=/var/lib/immich-postgres
```

---

# Deployment

Immich is deployed through Coolify using this repository.

## Coolify Notes

- Docker Compose resource
- Git-based deployments
- Bind mounts are required
- Do NOT use Docker-managed anonymous volumes for uploads or Postgres

---

# Backup Strategy

## Media Backup

```bash
rsync -aHAXv --delete \
  /mnt/storage/ \
  /mnt/storage-backup/
```

## PostgreSQL Backup

```bash
docker exec -t <postgres-container> pg_dumpall -U postgres \
  > ~/immich-backup.sql
```

---

# Restore Strategy

## Reuse Existing Database

Use the same bind mounts:

```env
UPLOAD_LOCATION=/mnt/storage/immich
DB_DATA_LOCATION=/var/lib/immich-postgres
```

Then redeploy Immich.

## Restore from SQL Dump

```bash
cat ~/immich-backup.sql | docker exec -i <postgres-container> psql -U postgres
```

---

# Cloudflare Tunnel

Coolify is exposed through Cloudflare Tunnel.

Example routes:

```text
coolify.example.com → http://localhost:8000
*.example.com       → http://localhost:80
```

Coolify proxy (Traefik) handles application routing.

---

# Migration History

## Storage Migration

Old:

```text
/mnt/immich-media
/mnt/backup
/opt/immich-app
```

New:

```text
/mnt/storage
/mnt/storage-backup
/opt/immich
```

## Coolify Migration

Migrated from:

- manual Docker Compose deployment

To:

- Git-based Coolify deployment

Existing uploads and PostgreSQL data were preserved using bind mounts.

---

# Operational Notes

## Before Deploying

Stop existing Immich stack:

```bash
docker compose down
```

## Validate After Deployment

- photos load
- uploads work
- mobile sync works
- existing users/albums exist

---

# Useful Commands

## View Containers

```bash
docker ps
```

## View Logs

```bash
docker logs -f <container>
```

## Docker Cleanup

```bash
docker system prune
```

---

# Future Improvements

- Move PostgreSQL data to `/mnt/storage/immich-postgres`
- Add scheduled Coolify backup jobs
- Add monitoring/alerting
- Add offsite backups
- Add automated DB dumps
