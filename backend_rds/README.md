# Створення мережі
docker network create my_network

# Запуск PostgreSQL контейнера
docker run -d --name postgres_db --network=my_network -e POSTGRES_DB=mydb -e POSTGRES_USER=myuser -e POSTGRES_PASSWORD=mypassword -p 5432:5432 postgres:13

# Запуск Backend RDS контейнера
docker run -d --name backend_rds --network=my_network -p 8000:8000 -e DB_NAME=mydb -e DB_USER=myuser -e DB_PASSWORD=mypassword -e DB_HOST=postgres_db -e DB_PORT=5432 -e CORS_ALLOWED_ORIGINS="http://localhost:8000,http://127.0.0.1:8000" backend_rds

# Запуск усіх сервісів через Docker Compose
docker-compose up -d

# Зупинка та видалення всіх сервісів
docker-compose down
