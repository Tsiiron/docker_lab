# backend/Dockerfile
FROM python:3.10-alpine

# Установка необходимых пакетов для работы с psycopg2 и миграциями
RUN apk add --no-cache python3-dev g++ make
RUN apk add --no-cache gcc musl-dev postgresql-dev libffi-dev \
    && pip install --no-cache-dir --upgrade pip

# Создание непривилегированного пользователя
RUN addgroup -S appgroup && adduser -S appuser -G appgroup

# Установка рабочей директории
WORKDIR /app

# Копирование файла зависимостей
COPY requirements.txt .

# Установка зависимостей
RUN pip install --no-cache-dir -r requirements.txt

# Копирование исходного кода
COPY . .

# Настройка прав доступа
RUN chown -R appuser:appgroup /app

# Переключение на непривилегированного пользователя
USER appuser

# Команда запуска
CMD ["python", "manage.py", "runserver"]