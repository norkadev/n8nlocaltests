# n8n Local Test Environment

This repository contains a Docker-based setup for running n8n (workflow automation tool) with PostgreSQL database locally for testing and development purposes.

## Files Overview

### `docker-compose.yml`
The main Docker Compose configuration file that defines two services:
- **postgres**: PostgreSQL 16 database server with health checks
- **n8n**: n8n workflow automation platform connected to the PostgreSQL database

The setup includes proper service dependencies, health checks, and volume persistence for both database data and n8n configurations.

### `init-data.sh`
A PostgreSQL initialization script that automatically runs when the database container starts for the first time. This script:
- Creates a dedicated non-root user for n8n to use
- Grants necessary database privileges to the n8n user
- Provides secure database access separation between admin and application users

### `.env`
Environment variables file containing PostgreSQL configuration:
- Database credentials for both root and application users
- Database name and connection parameters
- Used by both Docker Compose and the initialization script

## Features

- **Secure Database Setup**: Separate root and application database users
- **Health Checks**: Ensures PostgreSQL is ready before starting n8n
- **Data Persistence**: Database and n8n data persisted in Docker volumes
- **Easy Configuration**: Environment variables for customization

## Usage

To start the n8n environment with PostgreSQL:

```bash
docker-compose up -d
```

This command will:
1. Start PostgreSQL container and run the initialization script
2. Wait for database health check to pass
3. Start n8n container connected to the database
4. Make n8n available at http://localhost:5678

To stop the environment:

```bash
docker-compose down
```

## Notes

- n8n will be accessible at `http://localhost:5678`
- Database data persists in the `db_storage` Docker volume
- n8n configurations persist in the `n8n_storage` Docker volume
- Modify `.env` file to change database credentials or names