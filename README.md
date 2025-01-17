# README for Docker Compose and CI/CD Configuration

## Overview

This project includes two primary backend services, `backend_rds` and `backend_redis`, each running in its own Docker container. These services are orchestrated using `docker-compose`, along with PostgreSQL and Redis databases. Additionally, CI/CD pipelines have been configured to automate deployment processes.

## Services

### Backend RDS (`backend_rds`)
- **Description**: Manages user data and application logic.
- **Exposed Port**: 8000
- **Environment Variables**:
  - `DATABASE_URL`: PostgreSQL connection string.

### Backend Redis (`backend_redis`)
- **Description**: Manages caching and session storage.
- **Exposed Port**: 8001
- **Environment Variables**:
  - `REDIS_URL`: Redis connection string.

### PostgreSQL Database (`postgres_db`)
- **Description**: Stores persistent user and application data.
- **Exposed Port**: 5432

### Redis Database (`redis_db`)
- **Description**: Provides caching for faster responses.
- **Exposed Port**: 6379

## Usage

### Prerequisites
Ensure that Docker and Docker Compose are installed on your system.

### Starting the Services
To start all services, run:
```bash
docker-compose up -d
```

### Stopping the Services
To stop all services, run:
```bash
docker-compose down
```

### Logs
To view logs for all containers, run:
```bash
docker-compose logs
```

## CI/CD Pipeline

### Overview
The CI/CD pipelines are configured using GitHub Actions to automate testing, building, and deployment of the application.

### Pipeline Stages
1. **Testing**: Ensures the application passes all unit and integration tests.
2. **Build**: Creates Docker images for the backend services.
3. **Deployment**:
   - Pushes Docker images to a container registry.
   - Deploys updated services to the EC2 instance using `docker-compose`.

### CI/CD Configuration Files
- **GitHub Actions Workflow File**: `.github/workflows/ci-cd-backend.yml`

### Example Workflow Steps
1. **Install Dependencies**:
   ```yaml
   - name: Install Dependencies
     run: |
       pip install -r requirements.txt
   ```
2. **Run Tests**:
   ```yaml
   - name: Run Tests
     run: pytest
   ```
3. **Build Docker Images**:
   ```yaml
   - name: Build Docker Images
     run: docker-compose build
   ```
4. **Deploy Services**:
   ```yaml
   - name: Deploy
     run: |
       ssh -i ${{ secrets.EC2_KEY }} ec2-user@${{ secrets.EC2_HOST }} "cd ~/project && docker-compose up -d"
   ```

## Additional Notes

### Security
- Ensure that sensitive information, such as database credentials and secret keys, is stored securely using environment variables or secret management tools.

### Troubleshooting
- If a container fails to start, check the logs using:
  ```bash
  docker-compose logs <service_name>
  ```
- Verify the `.env` file contains all required variables.

### Scaling
- To scale services, update the `docker-compose.yml` file and add additional replicas using the `replicas` directive.
