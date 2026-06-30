# 🚀 Deploy to Coolify

1. 📁 Create a new project.
2. ➕ Create a new resource.
3. 🔐 Select `Private Repository (with GitHub App)`.
4. 🐙 Select GitHub App `zhunio-coolify`.
5. 📦 Select the `immich` repository.
6. ⚙️ Configure:
   - 🌿 Branch: `main`
   - 🐳 Build Pack: `Docker Compose`
   - 📄 Docker Compose Location: `/docker-compose.yml`
7. 🏷️ Set:
   - **Name:** `immich`
   - **Domain:** `https://photos.example.com`
8. 💾 Verify the host storage directories:
   - `/mnt/storage/immich`
   - `/var/lib/immich-postgres`

9. 🔑 Configure the required environment variables.
10. 🚀 Click **Deploy**.

## 🔑 Environment Variables

```env
UPLOAD_LOCATION=/mnt/storage/immich
DB_DATA_LOCATION=/var/lib/immich-postgres
```
