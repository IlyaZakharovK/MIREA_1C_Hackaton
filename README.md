# MeowHack 2024 2 Backend

Backend-сервис на FastAPI для работы с пользователями учебной системы: студенты, преподаватели и общие (neutral) эндпоинты.

## Стек

- Python 3.12
- FastAPI
- Uvicorn
- PostgreSQL (через `psycopg2`)
- JWT (`PyJWT`)

## Структура проекта

- `app/endpoints/` - HTTP-эндпоинты сервиса
- `app/db/` - слой работы с базой данных
- `app/models/` - Pydantic-модели запросов и ответов
- `app/tokens/` - логика декодирования токенов
- `settings.py` - конфигурация приложения из `.env`
- `run.py` - локальный запуск приложения

## Установка

1. Клонируйте репозиторий.
2. Создайте и активируйте виртуальное окружение.
3. Установите зависимости:

```bash
pip install -r requirements.txt
```

## Настройка окружения

Создайте файл `.env` в корне проекта и добавьте:

```env
APP_PORT=8000
SECRET_KEY=your_secret_key

DB_NAME=your_db_name
DB_USER=your_db_user
DB_PASSWORD=your_db_password
DB_HOST=localhost
DB_PORT=5432

JWT_ALGORITHM=HS256
ACCESS_TOKEN_EXPIRE_MINUTES=15
REFRESH_TOKEN_EXPIRE_HOURS=1
```

## Запуск

### Вариант 1 (через `run.py`)

```bash
python run.py
```

Скрипт дополнительно генерирует документацию в папке `docs/`.

### Вариант 2 (напрямую через Uvicorn)

```bash
uvicorn app.__init__:app --host 0.0.0.0 --port 8000 --reload
```

## API-префиксы

Все роуты подключены с базовым префиксом `/api/users`:

- `/api/users` - базовые маршруты (`main`)
- `/api/users/student` - маршруты студента
- `/api/users/teacher` - маршруты преподавателя
- `/api/users/neutral` - общие маршруты

Большинство эндпоинтов требуют заголовок:

`Authorization: <token>`

## Пути по всем веткам репозитория

Ниже перечислены пути, найденные во всех ветках через анализ `app/__init__.py` и `app/endpoints/*.py`.

### `UsersMicroservice` и `origin/UsersMicroservice`

Префиксы:
- `/api/users`
- `/api/users/student`
- `/api/users/teacher`
- `/api/users/neutral`

Пути:
- `GET /`
- `GET /lessons`
- `GET /info`
- `GET /gpa`
- `GET /grade`
- `GET /percentile`
- `POST /add/custom/lesson`
- `GET /custom/lessons`
- `GET /groups`
- `POST /mark`
- `GET /student/{student_code}`
- `GET /lessons`
- `POST /marking/students`
- `GET /disciplines`
- `GET /group/{group_code}`
- `GET /all/grades`
- `POST /add/task`
- `GET /lesson/{lesson_id}`
- `GET /entrances`
- `GET /enter/token`

### `LoginMicroservice` и `origin/LoginMicroservice`

Префиксы:
- `/api/auth/admin`
- `/api/auth/student`
- `/api/auth/teacher`

Пути:
- `POST /login`
- `GET /refresh`
- `POST /reset`
- `PUT /reset/confirm`

### `entranceMicroservice` и `origin/entranceMicroservice`

Префикс:
- `/api/entrance`

Пути:
- `POST /add`
- `POST /auditory/open`
- `PUT /auditory/close`

### `adminMicroservice`, `origin/adminMicroservice`, `main`, `origin/main`, `sdfhgsd/main`

В этих ветках API-пути в формате FastAPI-декораторов (`app/endpoints/*.py`) не обнаружены.

## Документация API

После запуска доступны:

- Swagger UI: `http://localhost:<APP_PORT>/docs`
- ReDoc: `http://localhost:<APP_PORT>/redoc`
- Сгенерированные файлы: `docs/index.html`, `docs/swagger.json`

## Лицензия

Проект распространяется по лицензии MIT. Подробности в файле `LICENSE`.
