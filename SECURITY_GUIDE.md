# Security Guide for Docker Compose Stacks

## Overview
This guide explains how to securely manage passwords, API keys, and other sensitive configuration in your Docker Compose environments.

## Environment Files (.env)

Each stack now includes a `.env` file for managing sensitive configuration:

- **`/lempstack/.env`** - Database credentials for MySQL and phpMyAdmin
- **`/caddy/.env`** - ACME/Let's Encrypt configuration
- **`/mediaserver/.env`** - API keys and user settings for media services
- **`/factorio/.env`** - Game server configuration and credentials

## Before Production Deployment

### 1. Change All Dummy Passwords
Replace all dummy passwords with strong, unique passwords:

```bash
# Example for LEMP stack
cd lempstack
cp .env .env.backup
nano .env  # Edit with strong passwords
```

### 2. Generate Strong Passwords
Use a password manager or generate secure passwords:

```bash
# Generate a 32-character password
openssl rand -base64 32

# Or use pwgen if available
pwgen -s 32 1
```

### 3. Set Proper File Permissions
Restrict access to .env files:

```bash
chmod 600 */.env
```

## Environment-Specific Configuration

### Development Environment
Keep the dummy passwords for local development:
```bash
# Use default .env files as-is
docker compose up -d
```

### Production Environment
Create production-specific environment files:

```bash
# Copy and customize for production
cp .env .env.production
# Edit .env.production with real credentials
# Use: docker compose --env-file .env.production up -d
```

### Staging Environment
Create staging-specific configurations:

```bash
cp .env .env.staging
# Edit .env.staging with staging credentials
# Use: docker compose --env-file .env.staging up -d
```

## Security Best Practices

### 1. Never Commit Real Passwords
- ✅ Use dummy passwords in version control
- ❌ Never commit actual production passwords
- ✅ Use `.gitignore` to exclude sensitive .env files

### 2. Use Different Passwords Per Environment
- **Development**: Dummy passwords (already provided)
- **Staging**: Different passwords from production
- **Production**: Strong, unique passwords

### 3. Regular Password Rotation
- Change passwords regularly (quarterly recommended)
- Update .env files and restart services
- Keep backup of previous configurations

### 4. Access Control
- Limit who has access to production .env files
- Use proper file permissions (600 or 640)
- Consider using secrets management tools for production

## Service-Specific Security Notes

### LEMP Stack (lempstack)
- Change `MYSQL_ROOT_PASSWORD` before production
- Consider creating non-root MySQL users for applications
- Restrict phpMyAdmin access (firewall/VPN only)

### Caddy (caddy)
- Configure real domain names in production
- Set up proper email for Let's Encrypt notifications
- Review Caddyfile for security headers

### Media Server (mediaserver)
- Set proper PUID/PGID for file permissions
- Configure API keys for automation
- Restrict access to admin interfaces

### Factorio (factorio)
- Set server password for private games
- Configure proper admin credentials
- Use factorio.com token for public servers

## Troubleshooting

### Environment Variables Not Loading
1. Check file permissions: `ls -la .env`
2. Verify file format (no spaces around =)
3. Restart containers: `docker compose down && docker compose up -d`

### Password Changes Not Applied
1. Stop services: `docker compose down`
2. Update .env file
3. Restart: `docker compose up -d`
4. Check logs: `docker compose logs`

## Advanced Security

### Using Docker Secrets (Swarm Mode)
For production deployments, consider Docker Secrets:

```yaml
secrets:
  mysql_password:
    external: true
services:
  mysql:
    secrets:
      - mysql_password
```

### External Secrets Management
Consider integrating with:
- HashiCorp Vault
- AWS Secrets Manager
- Azure Key Vault
- Kubernetes Secrets

## Support and Questions

If you encounter issues with environment variable configuration:
1. Check the Docker Compose documentation
2. Verify .env file syntax
3. Test with dummy values first
4. Review service logs for authentication errors

Remember: Security is a continuous process, not a one-time setup!