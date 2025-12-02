Multiple Containers Environment - Docker Compose Project
<p align="center"> <a href="http://nestjs.com/" target="blank"><img src="https://nestjs.com/img/logo-small.svg" width="120" alt="Nest Logo" /></a> </p>
🎯 Project Overview
This repository demonstrates a multi-container Docker environment running:

Node.js/NestJS API (containerized application)

MySQL Database (containerized database service)

The project showcases Docker container orchestration using Docker Compose to run multiple services that communicate with each other in an isolated development environment.

🏗️ Architecture
text
┌─────────────────────────────────────────────┐
│         Docker Compose Environment          │
├─────────────────┬───────────────────────────┤
│   Node.js API   │        MySQL Database     │
│   Container     │        Container          │
│   (Port: 3000)  │        (Port: 3306)       │
└─────────────────┴───────────────────────────┘
🚀 Quick Start
Prerequisites
Docker installed

Docker Compose installed

Running the Application
bash
# Clone the repository
git clone <your-repository-url>
cd MultipleContainersAmbient

# Start all containers
docker-compose up -d

# View running containers
docker-compose ps

# View logs
docker-compose logs -f api
Access the Application
API: http://localhost:3000

MySQL: localhost:3306

MySQL Credentials (defined in docker-compose.yml):

Username: root

Password: rootpassword

Database: mydatabase

📁 Project Structure
text
├── src/                    # NestJS API source code
├── Dockerfile             # Node.js API container configuration
├── docker-compose.yaml    # Multi-container orchestration
├── .dockerignore          # Docker ignore patterns
└── package.json          # Node.js dependencies
🔧 Container Details
1. API Container (api)
Base Image: Node.js 18

Port: 3000 → 3000

Build Context: Current directory

Environment Variables: Loaded from docker-compose

Dependencies: Installed via npm

Health Check: Monitors API availability

2. MySQL Container (db)
Base Image: MySQL:8.0

Port: 3306 → 3306

Persistent Volume: mysql_data

Default Database: mydatabase

Root Password: rootpassword

Auto-initialization: Database created on first run

📝 Docker Configuration Files
Dockerfile
dockerfile
FROM node:18-alpine
WORKDIR /usr/src/app
COPY package*.json ./
RUN npm install
COPY . .
RUN npm run build
EXPOSE 3000
CMD ["npm", "run", "start:prod"]
docker-compose.yaml
yaml
version: '3.8'
services:
  api:
    build: .
    ports:
      - "3000:3000"
    depends_on:
      db:
        condition: service_healthy
    environment:
      - DB_HOST=db
      - DB_PORT=3306
      - DB_USERNAME=root
      - DB_PASSWORD=rootpassword
      - DB_DATABASE=mydatabase
  
  db:
    image: mysql:8.0
    ports:
      - "3306:3306"
    environment:
      MYSQL_ROOT_PASSWORD: rootpassword
      MYSQL_DATABASE: mydatabase
    volumes:
      - mysql_data:/var/lib/mysql
    healthcheck:
      test: ["CMD", "mysqladmin", "ping", "-h", "localhost"]

volumes:
  mysql_data:
🛠️ Development Commands
bash
# Build containers
docker-compose build

# Start services in background
docker-compose up -d

# Stop services
docker-compose down

# Stop and remove volumes
docker-compose down -v

# Rebuild and restart
docker-compose up -d --build

# Access MySQL container
docker-compose exec db mysql -u root -p

# Access API container shell
docker-compose exec api sh

# View real-time logs
docker-compose logs -f

# Check container status
docker-compose ps
🌐 API Endpoints
Once running, test these endpoints:

bash
# Hello World endpoint
curl http://localhost:3000/

# Health check
curl http://localhost:3000/health
💾 Database Persistence
The MySQL data is persisted using Docker volumes:

Volume Name: mysql_data

Location: /var/lib/mysql inside container

Persistence: Data survives container restarts

To backup data:

bash
docker-compose exec db mysqldump -u root -prootpassword mydatabase > backup.sql
🔍 Troubleshooting
Common Issues
Port already in use

bash
# Check what's using port 3000 or 3306
netstat -ano | findstr :3000
MySQL connection refused

bash
# Check if MySQL container is healthy
docker-compose ps

# View MySQL logs
docker-compose logs db
Container build errors

bash
# Clean build
docker-compose build --no-cache
Permission issues

bash
# Reset Docker containers
docker system prune -a
📚 Learning Objectives
This project demonstrates:

Multi-container Docker environments

Service communication between containers

Docker Compose orchestration

Database containerization with persistence

Environment variable management

Health checks and dependency management

Production-ready Docker configurations

🔄 CI/CD Integration Ready
This setup is prepared for CI/CD pipelines with:

Pre-configured Docker images

Environment variable management

Health check endpoints

Database migration support

📄 License
This project is MIT licensed.

👨‍💻 Author
Kaue Fernandes

GitHub: @developerkaue

Email: kauecaobiancofernandes2@gmail.com

🤝 Contributing
Feel free to submit issues and enhancement requests!

Note: This is a demonstration project focusing on Docker container orchestration. The API is a simple NestJS starter with added database connectivity examples.
