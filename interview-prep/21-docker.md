# 21. DOCKER

## 21.1 What is Docker?
Docker packages applications into **containers** — lightweight, portable, self-sufficient environments that run anywhere.

## 21.2 Key Concepts

```
Image  → Blueprint (recipe)
Container → Running instance (the dish)
Dockerfile → Instructions to build image
Docker Compose → Define multi-container apps
```

### Dockerfile
**What:** A Dockerfile is a text file with step-by-step instructions to build a Docker image, specifying the base OS, dependencies, source code, and startup command.
**Why:** Interviewers expect you to write production-ready Dockerfiles with multi-stage builds, non-root users, and layer caching to demonstrate containerization best practices.

```dockerfile
# Multi-stage build (smaller final image)
FROM node:20-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .
RUN npm run build

FROM node:20-alpine
WORKDIR /app
COPY --from=builder /app/dist ./dist
COPY --from=builder /app/node_modules ./node_modules
COPY package*.json ./

EXPOSE 3000
USER node
CMD ["node", "dist/main.js"]
```

### Docker Compose
**What:** Docker Compose is a tool that defines and runs multi-container applications using a single YAML file, managing networking, volumes, and service dependencies.
**Why:** Interviewers ask about Compose to verify you can set up local development environments with databases, caches, and your app running together with one command.

```yaml
version: '3.8'
services:
  api:
    build: .
    ports: ["3000:3000"]
    environment:
      - DATABASE_URL=postgres://user:pass@db:5432/mydb
      - REDIS_URL=redis://redis:6379
    depends_on: [db, redis]

  db:
    image: postgres:15-alpine
    volumes: ["pgdata:/var/lib/postgresql/data"]
    environment:
      POSTGRES_DB: mydb
      POSTGRES_PASSWORD: pass

  redis:
    image: redis:7-alpine

  mongo:
    image: mongo:7
    volumes: ["mongodata:/data/db"]

volumes:
  pgdata:
  mongodata:
```

### Common Commands
**What:** Essential Docker CLI commands for building images, running/stopping containers, viewing logs, and managing multi-container setups.
**Why:** Interviewers may ask you to debug a running container or explain how you'd inspect logs and shell into a container in production.

```bash
docker build -t myapp .           # Build image
docker run -p 3000:3000 myapp     # Run container
docker ps                         # List running containers
docker logs <container>           # View logs
docker exec -it <container> sh    # Shell into container
docker-compose up -d              # Start all services
docker-compose down               # Stop all services
```

