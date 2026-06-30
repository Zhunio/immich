# 📸 Immich Photo Management

Self-hosted photo and video management platform with automatic backups, mobile synchronization, AI-powered search, and facial recognition.

## ✨ Features

- 📸 Self-hosted photo and video library.
- 📱 Automatic mobile photo backup.
- 🤖 AI-powered facial recognition and smart search.
- 🗺️ Timeline, albums, favorites, and sharing.
- 🎥 Automatic thumbnail and video transcoding.
- 🗄️ PostgreSQL database with vector search support.
- ❤️ Machine learning services for image analysis.
- 🐳 Run with Docker Compose or Coolify.

## 🚀 Coolify

Deploy this repository as a Docker Compose service.

- 🔐 Repository Type: `Private Repository (with GitHub App)`
- 🐙 GitHub App: `zhunio-coolify`
- 🌿 Branch: `main`
- 🐳 Build Pack: `Docker Compose`
- 🌐 Domain: `photos.example.com`
- 📂 Data mounts:
  - `/mnt/storage/immich`
  - `/var/lib/immich-postgres`
- 🔑 Environment variables:
  - `UPLOAD_LOCATION`
  - `DB_DATA_LOCATION`

For detailed deployment instructions, see [`DEPLOY.md`](DEPLOY.md).

## ⚙️ Immich Configuration

Configure Immich using Coolify environment variables.

### Required

- 📂 **UPLOAD_LOCATION** — Root directory for uploaded photos, videos, thumbnails, and generated files.
- 🗄️ **DB_DATA_LOCATION** — PostgreSQL data directory.

Example:

```env
UPLOAD_LOCATION=/mnt/storage/immich
DB_DATA_LOCATION=/var/lib/immich-postgres
```

## 💾 Storage Layout

Immich stores all uploaded media beneath `UPLOAD_LOCATION`.

```text
UPLOAD_LOCATION/
├── backups/
├── encoded-video/
├── library/
├── profile/
├── thumbs/
└── upload/
```

## ♻️ Restore

Restore consists of:

1. 🛑 Stop the application.
2. ☁️ Restore `/mnt/storage/immich`.
3. ☁️ Restore the PostgreSQL data directory.
4. 🚀 Start the application.

See [RESTORE.md](RESTORE.md).
