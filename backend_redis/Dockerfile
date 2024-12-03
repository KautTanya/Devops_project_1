# Вибираємо базовий образ Python
FROM python:3.9-slim

# Встановлюємо робочий каталог у контейнері
WORKDIR /app

# Копіюємо файл requirements.txt у контейнер
COPY requirements.txt .

# Встановлюємо залежності
RUN pip install --no-cache-dir -r requirements.txt

# Копіюємо решту файлів у контейнер
COPY . .

# Встановлюємо змінну оточення для Django
ENV DJANGO_SETTINGS_MODULE=backend_redis.settings

# Експонуємо порт 8000
EXPOSE 8000

# Команда для запуску Django-сервера
CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]
