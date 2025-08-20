# Vextra Quickstart

This is a Docker Compose configuration collection for quickly starting a complete Vextra ecosystem. With this configuration, you can start a complete development environment with all necessary services with one click.

## 🚀 Quick Start

### Prerequisites

- Docker and Docker Compose
- At least 4GB available memory
- At least 10GB available disk space

### Starting Services

```bash
# Start all services
./docker-run.sh up

# Stop all services
./docker-run.sh down

# Reset and restart all services
./docker-run.sh reset
```

## 🏗️ System Architecture

This quickstart configuration includes the following core services:

### Core Services
- **Vextra Server** - Main document processing server (port 80)
- **Auth Server** - Identity authentication service (port 81)
- **MCP Server** - Model Context Protocol service (port 82)

### Infrastructure Services
- **MySQL 8.0** - Main database (port 3306)
- **MongoDB 8.0** - Document database (port 27017)
- **Redis 8.0** - Cache and session storage (port 6379)
- **MinIO** - Object storage service (API port 9000, console port 9001)

## 📁 Directory Structure

```
quickstart/
├── README.md                    # This document
├── docker-compose.yaml          # Docker Compose configuration
├── docker-run.sh               # Convenient startup script
├── config/                     # Configuration file directory
│   ├── config-vextra-server.yaml  # Vextra server configuration
│   ├── config-auth.yaml           # Authentication service configuration
│   └── config-mcp.yaml            # MCP service configuration
└── scripts/                    # Initialization scripts
    ├── create-multiple-dbs.sh     # MySQL multi-database creation script
    └── minio-init.sh              # MinIO initialization script
```

## ⚙️ Configuration Details

### Vextra Server Configuration
- Database connections: MySQL + MongoDB
- Object storage: MinIO
- Document update service: Supports real-time document generation
- Cross-origin support: CORS enabled

### MinIO Configuration
- Default user: `root` / `your-password`
- Pre-created storage buckets:
  - `document` - Document storage
  - `attatch` - Attachment storage
  - `mcp` - MCP service storage
- Version control: Version control enabled for document bucket

### Database Configuration
- **MySQL**: Automatically creates `kcauth` and `kcserver` databases
- **MongoDB**: Default database `kcserver`
- **Redis**: Persistent storage with AOF support

## 🔧 Custom Configuration

### Modifying Port Mappings
Modify the `ports` configuration for each service in `docker-compose.yaml`:

```yaml
ports:
  - "8080:80"  # Map Vextra service to port 8080
```

### Modifying Database Passwords
1. Update environment variables in `docker-compose.yaml`
2. Update connection strings in corresponding configuration files
3. Restart services

### Adding New Storage Buckets
Add new bucket creation logic in `scripts/minio-init.sh`.

## 🚨 Important Notes

1. **Network Configuration**: Ensure Docker network `kcserver` can be created normally
2. **Port Conflicts**: Check if ports are occupied by other services
3. **Data Persistence**: All data is stored in Docker volumes and won't be lost on restart
4. **Memory Usage**: First startup may take a long time, please be patient

## 🐛 Troubleshooting

### Service Startup Failure
```bash
# Check service status
docker-compose ps

# View service logs
docker-compose logs [service-name]

# Recreate network
docker network rm kcserver
./docker-run.sh reset
```

### Database Connection Issues
```bash
# Check MySQL status
docker exec mysql mysqladmin ping -h localhost -u root -ppassword

# Check MongoDB status
docker exec mongo mongosh --eval "db.adminCommand('ping')"
```

### MinIO Access Issues
```bash
# Check MinIO status
curl http://localhost:9000/minio/health/live

# View MinIO logs
docker-compose logs minio
```

## 📚 Related Links

- [Vextra Core](https://github.com/kcaitech/vextra-core.git) - Core library
- [Vextra Server](https://github.com/kcaitech/vextra-server.git) - Server implementation
- [Vextra Editor](https://github.com/kcaitech/vextra-editor.git) - Editor
- [Vextra MCP](https://github.com/kcaitech/vextra-mcp.git) - MCP service

## 📄 License

This project is licensed under the [LICENSE](./LICENSE.txt) license.
