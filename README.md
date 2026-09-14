# WordPress + Docker + Bedrock

A modern WordPress development stack using Docker Compose and [Roots Bedrock](https://roots.io/bedrock/).

---

## 🚀 Quick Start

### Requirements
- [Docker Desktop](https://www.docker.com/products/docker-desktop/) installed and running
- Git (optional)

### Setup Instructions

1. Open a terminal in the project root directory.
2. Copy environment files:
   - **Windows PowerShell**:
     ```powershell
     Copy-Item .env.example .env
     Copy-Item site/.env.example site/.env
     ```
   - **Linux / macOS / Bash**:
     ```bash
     cp .env.example .env
     cp site/.env.example site/.env
     ```
3. Build PHP & containers:
   ```bash
   docker compose build
   ```
4. Install Bedrock dependencies:
   ```bash
   docker compose run --rm php composer install
   ```
5. Start containers:
   ```bash
   docker compose up -d
   ```

---

## 🔗 Access Links & Credentials

### Site Links
- **Website URL**: [http://localhost:8080](http://localhost:8080)
- **WP Admin URL**: [http://localhost:8080/wp/wp-admin](http://localhost:8080/wp/wp-admin)

### WP Admin Credentials
- **Username**: `admin`
- **Password**: `admin`

### Database Details
- **Host (Internal Container)**: `db`
- **Port**: `3306`
- **Database Name**: `wordpress`
- **User**: `wordpress`
- **Password**: `wordpress`
- **Root Password**: `change-root-password`

---

## 📁 Project Structure

```
wordpress-bedrock-docker/
├── docker/                     # Docker configuration files
│   ├── nginx/
│   │   └── default.conf        # Nginx virtual host configuration (points root to /web)
│   └── php/
│       └── Dockerfile          # Custom PHP 8.3 FPM image with extensions & WP-CLI
├── site/                       # Bedrock WordPress root directory
│   ├── config/                 # Environment-specific configuration files
│   │   ├── application.php     # Main Bedrock WP configuration (replaces wp-config.php)
│   │   └── environments/       # Environment overrides (development, staging, production)
│   ├── web/                    # Document root
│   │   ├── app/                # Custom content folder (replaces wp-content)
│   │   │   ├── mu-plugins/     # Must-use plugins
│   │   │   ├── plugins/        # WordPress plugins installed via Composer
│   │   │   └── themes/         # WordPress themes installed via Composer
│   │   ├── wp/                 # WordPress core installation directory
│   │   ├── index.php           # WordPress bootstrapper
│   │   └── wp-config.php       # Required wrapper for WP core
│   ├── .env                    # Environment variables for WordPress/Bedrock
│   └── composer.json           # Bedrock project & dependency manager
├── docker-compose.yml          # Docker Compose service definition
├── .env                        # Environment variables for Docker services
└── README.md                   # Project documentation
```

---

## 🛠️ Useful Commands

- **View Logs**:
  ```bash
  docker compose logs -f nginx
  docker compose logs -f php
  ```
- **Run WP-CLI**:
  ```bash
  docker compose exec php wp <command> --allow-root
  # Example: check WP CLI info
  docker compose exec php wp --info --allow-root
  ```
- **Stop Containers**:
  ```bash
  docker compose down
  ```
- **Stop and Reset Database Volume**:
  ```bash
  docker compose down -v
  ```
  *(⚠️ Warning: This completely deletes the database volume)*
