# Створення мережі
docker network create my_network

# Запуск Redis контейнера
docker run -d \
  --name redis_db \
  --network=my_network \
  -p 6379:6379 \
  redis:6.2

# Запуск Backend Redis контейнера
docker run -d \
  --name backend_redis \
  --network=my_network \
  -p 8001:8000 \
  -e REDIS_HOST=redis_db \
  -e REDIS_PORT=6379 \
  -e CORS_ALLOWED_ORIGINS="http://localhost:8001,http://127.0.0.1:8001" \
  backend_redis

# Запуск усіх сервісів через Docker Compose
docker-compose up -d

# Зупинка та видалення всіх сервісів
docker-compose down
