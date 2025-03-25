# MongoDB with Mongo-Express Docker Stack

![MongoDB Logo](https://webassets.mongodb.com/_com_assets/cms/mongodb_logo1-76twgcuytd.png) ![Mongo-Express Logo](https://raw.githubusercontent.com/mongo-express/mongo-express/master/img/logo.png)

A Docker Compose setup for MongoDB with Mongo-Express admin interface.  
Maintained by [@mihamieat](https://github.com/mihamieat)

## Features
- Latest MongoDB image container with persistent storage
- Latest Mongo-Express image web admin interface
- Secure authentication for both services
- Automatic restart on failure

## Prerequisites
- Docker
- Docker Compose

## Environment Variables

Create a `.env` file in the same directory with these variables:

| Variable Name                  | Required | Description                                                                 | Example Value       |
|--------------------------------|----------|-----------------------------------------------------------------------------|---------------------|
| `DB_ROOT_USERNAME`             | Yes      | Admin username for MongoDB                                                  | `admin`             |
| `DB_ROOT_PASSWORD`             | Yes      | Admin password for MongoDB (min 8 chars)                                    | `SecurePass123!`    |
| `DB_UI_AUTH_USERNAME`          | No       | Basic auth username for Mongo-Express UI (default: none)                    | `uiadmin`           |
| `DB_UI_AUTH_PASSWORD`          | No       | Basic auth password for Mongo-Express UI (default: none)                    | `UISecret456!`      |

## Quick Start

1. Create `.env` file with the environment variables specified above.
2. Start service
```sh
docker compose up -d
```

## Backup Strategy
```sh
# Create backup
docker exec mongodb mongodump --archive --gzip > backup.gz

# Restore backup
cat backup.gz | docker exec -i mongodb mongorestore --archive --gzip
```