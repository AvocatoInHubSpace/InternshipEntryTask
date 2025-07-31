# Tic-Tac-Toe Game API

REST API для партий в крестики-нолики (tic-tac-toe) с гибкой логикой, валидацией и хранилищем на PostgreSQL.  
Использованы Clean Architecture, ASP.NET, Entity Framework, MediatR, xUnit и Docker.

---

## 🚀 Возможности

- Создание партий с произвольным размером поля
- Ходы по очереди (с элементом случайности каждые 3 хода — возможна инверсия хода)
- Получение информации о партии и статусе (в процессе / ничья / победа X / победа O)
- Проверка валидности ходов, чёткие коды ошибок(ProblemDetails)
- Полная документация через Swagger

---

## 🛠️ Технологии

- **ASP.NET Core**
- **Entity Framework Core** (PostgreSQL)
- **MediatR**
- **xUnit**
- **Docker + Docker Compose**
- **Swagger**

---

## Быстрый старт

### 1. Клонировать репозиторий

bash
git clone https://github.com/your-username/tictactoe-api.git
cd tictactoe-api


### 2. Запуск через Docker Compose

bash
docker-compose up --build

- API по адресу: [http://localhost:8080](http://localhost:8080)
- Swagger UI: [http://localhost:8080/swagger](http://localhost:8080/swagger)

### 3. Локальный запуск

- Требуется .NET 9 SDK и PostgreSQL
- Все основные параметры — в `appsettings.json` и `docker-compose.yml`
- Миграции накатываются автоматически при первом запуске (`Development`-режим)

---

## API: Основные эндпоинты

- **POST `/api/games`** — создать игру

Ответ:

{
"id": 0,
"size": 3,
"winLineSize": 3,
"isXMove": true,
"state": "InProgress",
"field": "_________"
}



- **POST `/api/games/{gameId}/moves`** — сделать ход

json
{ "x": 1, "y": 2 }


Ответ:

json
{
"gameId": 1,
"isXMoved": true,
"state": "InProgress",
"x": 1,
"y": 2
}



- **GET `/api/games/{gameId}`** — получить состояние игры  
  Ответ:

json
{
"id": 0,
"size": 3,
"winLineSize": 3,
"isXMove": true,
"state": "InProgress",
"field": "_________"
}



- **GET `/health`** — для проверки статуса API

Подробная документация — в Swagger UI!

---

## 🎲 Особенности логики игры

- **Размер поля** и **длина выигрышной линии** задаются свободно (например 4х4, winLine 3 и т.п.)
- Игровое поле сохраняется строкой длины size×size (символы `'X'`, `'O'`, `'_'`)
- **Победа**: N подряд символов по горизонтали, вертикали или диагонали
- **Ходы выполняются по очереди**, но каждые 3 хода — случайная инверсия: игроки X и O могут поменяться (логика через random в move)
- Автоматическая проверка победы, ничьей, занятой клетки и выхода за пределы поля


---

## ⚙️ Настройки

- Все переменные подключения и параметры игры — через файлы appsettings*.json, env-переменные или docker-compose.yml:
    - POSTGRES_DB, POSTGRES_USER, POSTGRES_PASSWORD, DefaultConnection
- TicTacToeGameOptions — настройки логики (размер поля, выигрышная линия)

---

## 🧪 Тестирование

Запустить:

dotnet test


---

## 📖 Документация

- Swagger: /swagger
