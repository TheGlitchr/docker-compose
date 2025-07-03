# Docker Compose Stacks

Various Docker Compose files for server infrastructure, fully modernized and security-hardened.

## 🚀 Stacks Available

| Stack | Description | Services |
|-------|-------------|----------|
| **lempstack** | Linux, Nginx, MySQL, PHP | nginx, php-fpm, mysql, phpmyadmin |
| **mediaserver** | Complete media management | plex, sonarr, couchpotato, sabnzbd, deluge, mylar, etc. |
| **caddy** | Modern reverse proxy | caddy with automatic HTTPS |
| **factorio** | Game server | factorio dedicated server |

## ✨ Features

- **Modernized Syntax**: Updated to latest Docker Compose Specification
- **Security First**: All passwords externalized to `.env` files
- **Network Isolation**: Custom networks for each stack
- **Production Ready**: Proper restart policies and dependencies
- **Validated**: All files pass syntax validation

## 🔒 Security

Each stack includes a `.env` file with dummy passwords for development:

```bash
# Example usage
cd lempstack
docker compose up -d
```

**⚠️ IMPORTANT**: Change dummy passwords before production deployment!

See [`SECURITY_GUIDE.md`](SECURITY_GUIDE.md) for complete security instructions.

## 📁 Project Structure

```
├── lempstack/
│   ├── docker-compose.yml
│   └── .env                    # Database credentials
├── mediaserver/
│   ├── docker-compose.yml
│   └── .env                    # API keys and user settings
├── caddy/
│   ├── docker-compose.yaml
│   └── .env                    # ACME configuration
├── factorio/
│   ├── docker-compose.yaml
│   └── .env                    # Game server settings
├── SECURITY_GUIDE.md           # Comprehensive security guide
└── DOCKER_COMPOSE_CLEANUP_REPORT.md  # Modernization details
```

## 🚀 Quick Start

1. **Clone and enter directory**:
   ```bash
   git clone <repository>
   cd docker-compose
   ```

2. **Choose a stack and start**:
   ```bash
   cd lempstack  # or mediaserver, caddy, factorio
   docker compose up -d
   ```

3. **For production deployment**:
   - Read [`SECURITY_GUIDE.md`](SECURITY_GUIDE.md)
   - Update `.env` with strong passwords
   - Configure domain-specific settings

## 📋 Requirements

- Docker Engine 20.10+
- Docker Compose v2.0+
- Sufficient disk space for data volumes

## 🔧 Configuration

Each stack is pre-configured with sensible defaults:

- **Development**: Use included dummy passwords
- **Production**: Update `.env` files with real credentials
- **Custom**: Modify compose files as needed

## 📖 Documentation

- [`SECURITY_GUIDE.md`](SECURITY_GUIDE.md) - Password and secrets management
- [`DOCKER_COMPOSE_CLEANUP_REPORT.md`](DOCKER_COMPOSE_CLEANUP_REPORT.md) - Modernization details

## 🛠 Maintenance

To update a stack:
```bash
cd <stack-name>
docker compose pull
docker compose up -d
```

To view logs:
```bash
docker compose logs -f
```

## 🤝 Contributing

Feel free to submit issues and enhancement requests!

## 📄 License

Open source - use at your own discretion. Change passwords before production use!
