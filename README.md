# Docker Compose Configurations

This repository contains various Docker Compose configurations for different applications and services.

## 📁 Repository Structure

```
dockers/
├── README.md                    # This file
└── n8n-docker/                 # n8n with PostgreSQL setup
    ├── docker-compose.yml      # Docker Compose configuration
    ├── .env                    # Environment variables
    ├── README.md               # Detailed setup instructions
    └── .gitignore              # Git ignore rules
```

## 🚀 Available Configurations

### n8n with PostgreSQL
A complete workflow automation platform setup with PostgreSQL database backend.

**Location**: `n8n-docker/`

**Services**:
- **n8n**: Workflow automation platform (Port: 5678)
- **PostgreSQL**: Database backend (Port: 5432)

**Quick Start**:
```bash
cd n8n-docker
# Edit .env file with your preferred settings
docker-compose up -d
```

**Access**: http://localhost:5678

For detailed setup instructions, see [`n8n-docker/README.md`](n8n-docker/README.md)

## 🛠 Prerequisites

- Docker Engine 20.10+
- Docker Compose v2.0+


## 🌐 Shared Network Setup

Some services are configured to use a shared Docker network called `shared_network` so they can communicate across different compose projects.

**How to create and use the shared network:**

1. Create the network (only needed once):
   ```sh
   docker compose -f shared-network.yml up
   # or just create the network directly:
   docker network create shared_network
   ```
   The file `shared-network.yml` is provided in the repo for convenience.

2. Start your services as usual in their respective directories:
   ```sh
   docker compose up -d
   ```

All services using `shared_network` will be able to communicate with each other.

## 📋 General Usage

1. Navigate to the desired configuration directory
2. Copy and customize the `.env` file if present
3. Run `docker-compose up -d` to start services
4. Run `docker-compose down` to stop services

## 🔧 Common Commands

```bash
# Start services in detached mode
docker-compose up -d

# Stop services
docker-compose down

# Stop services and remove volumes (data will be lost)
docker-compose down -v

# View logs
docker-compose logs -f

# View logs for specific service
docker-compose logs -f <service-name>

# Check service status
docker-compose ps

# Restart services
docker-compose restart

# Pull latest images
docker-compose pull
```

## 📊 Monitoring & Maintenance

### Health Checks
Most configurations include health checks. Check service health with:
```bash
docker-compose ps
```

### Log Management
To view and manage logs:
```bash
# View all logs
docker-compose logs

# Follow logs in real-time
docker-compose logs -f

# View logs for last 100 lines
docker-compose logs --tail=100

# View logs for specific service
docker-compose logs <service-name>
```

### Data Backup
Each configuration may have different backup procedures. Refer to the specific README in each directory for backup instructions.

## 🔒 Security Considerations

1. **Environment Variables**: Always customize default passwords and secrets in `.env` files
2. **Network Access**: By default, services are accessible only on localhost
3. **Data Persistence**: Most configurations use Docker volumes for data persistence
4. **Updates**: Regularly update images for security patches

## 🐛 Troubleshooting

### Common Issues

1. **Port Conflicts**: 
   - Check if ports are already in use: `sudo lsof -i :PORT`
   - Modify port mappings in docker-compose.yml

2. **Permission Issues**:
   - Ensure Docker daemon is running
   - Check user permissions for Docker

3. **Memory Issues**:
   - Increase Docker memory limits
   - Monitor resource usage: `docker stats`

4. **Network Issues**:
   - Reset Docker networks: `docker network prune`
   - Check firewall settings

### Logs and Debugging
```bash
# View system-wide Docker events
docker events

# Inspect container details
docker inspect <container-name>

# Execute commands in running container
docker-compose exec <service-name> <command>

# Access container shell
docker-compose exec <service-name> /bin/bash
```

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Add your Docker Compose configuration in a new directory
4. Include a comprehensive README.md for your configuration
5. Test thoroughly
6. Submit a pull request

### Configuration Guidelines

When adding new configurations:

1. **Directory Structure**: Create a dedicated directory for each application
2. **Documentation**: Include a detailed README.md with setup instructions
3. **Environment Variables**: Use `.env` files for configuration
4. **Health Checks**: Implement health checks where applicable
5. **Data Persistence**: Use named volumes for data that should persist
6. **Security**: Use secure defaults and document security considerations

## 📄 License

This project is licensed under the MIT License.

## 📞 Support

For issues and questions:

1. Check the specific configuration's README
2. Review the troubleshooting section above
3. Search existing issues in the repository
4. Create a new issue with detailed information

## 🔄 Updates

This repository is actively maintained. Check back regularly for:
- New Docker Compose configurations
- Security updates
- Feature improvements
- Bug fixes

---

**Last Updated**: August 3, 2025
**Docker Compose Version**: 2.0+
**Docker Engine Version**: 20.10+
