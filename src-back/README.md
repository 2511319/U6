# SQL Proxy Server

TypeScript Node.js сервер для выполнения SQL запросов через HTTP API. Поддерживает PostgreSQL, MySQL и SQLite базы данных.

## Особенности

- 🔒 Выполняет только SELECT запросы для безопасности
- 🚦 Rate limiting для защиты от злоупотреблений
- 🌐 CORS поддержка
- 📊 Поддержка PostgreSQL, MySQL, SQLite
- ⚡ TypeScript с строгой типизацией
- 🔄 Автоматическое управление соединениями с БД

## Установка

```bash
npm install
```

## Запуск

### Разработка

```bash
npm run dev
```

### Продакшн

```bash
npm run build
npm start
```

## API

### POST /api/select

Выполняет SELECT запрос к базе данных.

**Тело запроса:**

```json
{
	"credentials": {
		"host": "localhost",
		"port": 5432,
		"username": "user",
		"password": "password",
		"database": "mydb",
		"type": "postgres",
		"ssl": false
	},
	"query": "SELECT * FROM users WHERE id = $1",
	"parameters": [1]
}
```

**Ответ:**

```json
{
	"success": true,
	"data": [{ "id": 1, "name": "John", "email": "john@example.com" }],
	"executionTime": 45,
	"rowCount": 1
}
```

### GET /health

Проверка состояния сервера.

## Поддерживаемые БД

- **PostgreSQL** (`type: "postgres"`)
- **MySQL** (`type: "mysql"`)
- **SQLite** (`type: "sqlite"`)

## Переменные окружения

Скопируйте `.env.example` в `.env` и настройте:

```bash
cp .env.example .env
```

## Rate Limiting

- **SQL запросы**: 10 запросов в минуту на IP
- **Общие запросы**: 100 запросов в минуту на IP

## Безопасность

- Разрешены только SELECT запросы
- Rate limiting по IP
- Автоматическое закрытие соединений с БД
- Валидация входных данных

## Разработка

```bash
# Форматирование кода
npm run format

# Проверка форматирования
npm run format:check

# Сборка проекта
npm run build
```
