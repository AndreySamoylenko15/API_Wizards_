# API Wizards

**API Wizards** — це сучасний REST API проєкт на Python (FastAPI), який надає готову архітектуру для створення веб-сервісів з авторизацією, роботою з користувачами, фото, коментарями та ролями.

## 🚀 Особливості
- Побудований на **FastAPI** — швидкий, асинхронний веб-фреймворк.
- JWT-автентифікація та авторизація.
- Робота з користувачами, ролями, фото та коментарями.
- Відправка email (включно з шаблоном в `src/services/templates/verify_email.html`).
- Підтримка **Alembic** для міграцій бази даних.
- Конфігурація для Docker / docker-compose.
- Документація Sphinx у папці `docs/`.

## 🧭 Структура проєкту (фрагмент)
/src
/routes # кінцеві точки (auth, user, photos, comments...)
/schemas # Pydantic-схеми
/services # логіка (auth, email, roles...)
/repository # робота з БД (CRUD)
main.py # точка входу
docker-compose.yml
alembic.ini # налаштування міграцій
.env.example # приклад змінних середовища
docs/ # Sphinx-документація
## ⚙️ Вимоги
- Python 3.10+ (див. pyproject.toml / requirements.txt)
- PostgreSQL (якщо використовуєте production-налаштування)
- (опціонально) Docker / docker-compose

## 🔧 Налаштування та локальний запуск

1. Скопіюйте `.env.example` в `.env` та налаштуйте змінні (DATABASE_URL, SECRET_KEY, SMTP тощо):

```env
DATABASE_URL=postgresql://user:password@localhost:5432/dbname
SECRET_KEY=your_secret_key
EMAIL_HOST=...
EMAIL_PORT=...
EMAIL_USER=...
EMAIL_PASS=...
Встановіть залежності:
pip install -r requirements.txt
# або якщо використовуєте poetry:
poetry install
Запустіть міграції Alembic:
alembic upgrade head
Запустіть сервер локально (uvicorn):
uvicorn main:app --reload --host 0.0.0.0 --port 8000
Відкрийте автоматичну документацію:

Swagger UI: http://localhost:8000/docs

ReDoc: http://localhost:8000/redoc
🐳 Запуск з Docker
docker-compose up --build
Це підніме сервіси (залежить від docker-compose.yml) і підключить базу даних, якщо вона описана у файлі.

📚 Документація
Документація проєкту розташована у папці docs/. Щоб зібрати локально Sphinx документацію, перейдіть до docs/ і запустіть make html (або make.bat для Windows).
