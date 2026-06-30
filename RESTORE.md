# ♻️ Restore

1. 🛑 Stop the application.

   ```bash
   docker compose down
   ```

2. ☁️ Restore `/mnt/storage/immich` using the `backups` service.

3. 🗄️ Start PostgreSQL.

   ```bash
   docker compose up -d immich-postgres
   ```

4. 📦 Restore the database.

   ```bash
   zstd -d /mnt/storage/immich/backups/latest-postgres_immich_immich-postgres.sql.zst
   ```

   ```bash
   psql -U postgres -d immich < /mnt/storage/immich/backups/latest-postgres_immich_immich-postgres.sql
   ```

5. 🚀 Start the application.

   ```bash
   docker compose up -d
   ```
