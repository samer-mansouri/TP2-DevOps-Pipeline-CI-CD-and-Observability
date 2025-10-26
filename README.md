# TP2 DevOps - Blogging App

Spring Boot blogging application with MySQL database, CI/CD pipeline, and complete observability stack.

## Features

- RESTful API with JWT authentication
- MySQL database with Docker support
- CI/CD pipeline with GitHub Actions (local development)
- Complete observability: Metrics (Prometheus), Logs (Loki), Traces (Zipkin)
- Grafana dashboards for monitoring
- Automated testing and security scanning

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

### Run with Complete Observability Stack
```bash
docker-compose -f docker-compose-observability.yml up -d --build
```

Wait 2-3 minutes for all services to start.

## Access Points

- Application: http://localhost:9090
- Swagger UI: http://localhost:9090/swagger-ui/
- Prometheus: http://localhost:9091
- Grafana: http://localhost:3000 (admin/admin)
- Zipkin: http://localhost:9411

## Docker Commands

```bash
# Start services
docker-compose up -d

# Start with observability
docker-compose -f docker-compose-observability.yml up -d

# View logs
docker logs tp2_devops_app -f
docker logs tp2_devops_mysql -f

# Stop services
docker-compose down
docker-compose -f docker-compose-observability.yml down

# Rebuild and start
docker-compose up -d --build
```

## Database Access

```bash
docker exec -it tp2_devops_mysql mysql -u root -psuperadmin123 blogging_app_apis
```

## Configuration

- Port: 9090
- Database: blogging_app_apis
- MySQL Port: 3306
- Credentials: root / superadmin123

## CI/CD Pipeline

The GitHub Actions pipeline runs automatically on push to main/develop branches:

1. Run unit and integration tests
2. Build application with Maven
3. Build Docker image
4. Security scanning with Trivy

No deployment stages - all development is done locally.

## Observability Stack

Three pillars of observability:

1. **Metrics** - Prometheus collects, Grafana visualizes
2. **Logs** - Loki aggregates, Promtail ships, Grafana queries
3. **Traces** - Zipkin for distributed tracing

### View Metrics
1. Open Grafana: http://localhost:3000 (admin/admin)
2. Navigate to Dashboards
3. Open "Blogging App - Spring Boot Metrics"

### View Logs
1. In Grafana, go to Explore
2. Select Loki datasource
3. Query: `{app="blogging-app-apis"}`

### View Traces
1. Open Zipkin: http://localhost:9411
2. Click "Run Query"
3. Select a trace to analyze

## Testing

```bash
# Run tests
./mvnw test

# Run with coverage
./mvnw test jacoco:report

# View coverage report
open target/site/jacoco/index.html
```

## Development Workflow

1. Make code changes
2. Push to GitHub (triggers CI/CD pipeline)
3. Pipeline runs tests and builds Docker image
4. Pull latest changes locally
5. Run with observability: `docker-compose -f docker-compose-observability.yml up -d --build`
6. Monitor in Grafana
7. View logs in Loki
8. Trace requests in Zipkin
