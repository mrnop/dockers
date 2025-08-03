# n8n with PostgreSQL Docker Setup

This Docker Compose setup provides a complete n8n workflow automation platform with PostgreSQL database.

## Services

- **n8n**: Workflow automation platform (http://localhost:5678)
- **PostgreSQL**: Database backend (localhost:5432)

## Quick Start

1. Navigate to the n8n-docker folder:
   ```bash
   cd n8n-docker
   ```
2. Update the `.env` file with your preferred settings
3. Start the services:
   ```bash
   docker-compose up -d
   ```

## Configuration

### Environment Variables

Edit the `.env` file to customize your installation:

- `POSTGRES_PASSWORD`: Change this to a secure password
- `N8N_HOST`: Set to your domain if exposing publicly
- `TIMEZONE`: Set your preferred timezone
- Basic auth settings for additional security

### Important Security Notes

1. **Change the default PostgreSQL password** in the `.env` file
2. If exposing to the internet, enable basic authentication by setting:
   - `N8N_BASIC_AUTH_ACTIVE=true`
   - `N8N_BASIC_AUTH_USER=your_username`
   - `N8N_BASIC_AUTH_PASSWORD=your_password`

## Usage

### Start Services
```bash
cd n8n-docker
docker-compose up -d
```

### Stop Services
```bash
cd n8n-docker
docker-compose down
```

### View Logs
```bash
cd n8n-docker
# All services
docker-compose logs -f

# Specific service
docker-compose logs -f n8n
docker-compose logs -f postgres
```

### Access n8n
Open your browser and navigate to: http://localhost:5678

### Database Access
The PostgreSQL database is accessible on `localhost:5432` with the credentials from your `.env` file.

## Data Persistence

- n8n data: Stored in `n8n_data` Docker volume
- PostgreSQL data: Stored in `postgres_data` Docker volume

## Backup

To backup your data:

```bash
# Backup n8n data
docker run --rm -v n8n_data:/data -v $(pwd):/backup alpine tar czf /backup/n8n_backup.tar.gz -C /data .

```bash
cd n8n-docker
# Backup PostgreSQL
docker-compose exec postgres pg_dump -U n8n -d n8n > n8n_database_backup.sql
```
```

## Troubleshooting

### Check service status
```bash
cd n8n-docker
docker-compose ps
```

### Check if services are healthy
```bash
cd n8n-docker
docker-compose exec postgres pg_isready -U n8n -d n8n
```

### Reset everything (WARNING: This will delete all data)
```bash
cd n8n-docker
docker-compose down -v
docker-compose up -d
```

## Customization

- To use a different PostgreSQL version, change the image tag in `docker-compose.yml`
- To use a different n8n version, change the image tag in `docker-compose.yml`
- Additional n8n environment variables can be added to the n8n service section
