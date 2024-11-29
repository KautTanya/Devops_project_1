# Використовуємо базовий образ Python
FROM python:3.9-slim

# Встановлюємо необхідні системні пакети
RUN apt-get update && apt-get install -y \
    build-essential \
    libpq-dev \
    && rm -rf /var/lib/apt/lists/*

# Встановлюємо робочу директорію
WORKDIR /app

# Копіюємо файл залежностей
COPY requirements.txt .

# Встановлюємо залежності Python
RUN pip install --no-cache-dir -r requirements.txt

# Копіюємо весь проєкт у контейнер
COPY . .

# Відкриваємо порт 8000 для доступу до додатку
EXPOSE 8000

# Команда для запуску сервера розробки Django
CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]
