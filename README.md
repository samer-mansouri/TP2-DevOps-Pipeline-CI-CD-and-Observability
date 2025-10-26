# TP2 DevOps - Blogging App

Spring Boot blogging application with MySQL database.

## Quick Start

### Run MySQL Only
```bash
docker-compose -f docker-compose-mysql.yml up -d
./mvnw spring-boot:run
```

### Run Full Stack (MySQL + App)
```bash
docker-compose up -d --build
```

Access at: http://localhost:9090

Swagger UI: http://localhost:9090/swagger-ui/

## Docker Commands

```bash
# Start services
docker-compose up -d

# View logs
docker logs tp2_devops_app -f
docker logs tp2_devops_mysql -f

# Stop services
docker-compose down

# Rebuild and start
docker-compose up -d --build
```

## Database Access

```bash
docker exec -it tp2_devops_mysql mysql -u root -psuperadmin123 blogging_app_apis
```

## Configuration

- **Port:** 9090
- **Database:** blogging_app_apis
- **MySQL Port:** 3306
- **Credentials:** root / superadmin123

