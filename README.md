# API Wizards

API Wizards is a FastAPI backend project for a photo-sharing service. It includes user authentication, JWT tokens, role-based access, photo metadata workflows, comments, tags, PostgreSQL migrations, and Docker-based local infrastructure.

The project is prepared to be reviewed and run locally without requiring a paid cloud deployment.

## Tech Stack

- Python 3.11+
- FastAPI
- SQLAlchemy async ORM
- PostgreSQL
- Alembic
- Docker Compose
- JWT authentication
- Cloudinary integration for photo storage and transformations
- Redis-ready configuration
- Swagger / OpenAPI documentation

## Features

- User signup and login
- JWT access and refresh tokens
- Email confirmation flow
- Roles: `admin`, `moderator`, `user`
- User profile lookup
- Photo upload and management
- Photo resize, crop, format conversion, filters, text overlay, metadata
- Comments for photos
- Tags for photos
- QR code generation for transformed photo links
- Database migrations with Alembic

## Project Structure

```text
.
|-- main.py
|-- src
|   |-- conf
|   |-- database
|   |-- repository
|   |-- routes
|   |-- schemas
|   `-- services
|-- migrations
|-- docs
|-- docker-compose.yml
|-- alembic.ini
|-- requirements.txt
|-- .env.example
`-- DEPLOYMENT.md
```

## Local Setup

Clone the repository:

```bash
git clone https://github.com/AndreySamoylenko15/API_Wizards_.git
cd API_Wizards_
```

Create `.env` from the example:

```bash
cp .env.example .env
```

For local development, use values like these:

```env
POSTGRES_DB=api_wizards
POSTGRES_USER=api_wizards
POSTGRES_PASSWORD=api_wizards
POSTGRES_PORT=5432
POSTGRES_DOMAIN=localhost

SECRET_KEY_JWT=local_dev_secret_key_change_me
ALGORITHM=HS256

MAIL_USERNAME=dev@example.com
MAIL_PASSWORD=dev_password
MAIL_FROM=dev@example.com
MAIL_PORT=587
MAIL_SERVER=localhost

REDIS_DOMAIN=localhost
REDIS_PORT=6379
REDIS_PASSWORD=

cloud_name=
api_key=
api_secret=
```

Start PostgreSQL and Redis:

```bash
docker compose up -d
```

Install dependencies:

```bash
python -m pip install -r requirements.txt
```

Apply migrations:

```bash
python -m alembic upgrade head
```

Run the API:

```bash
python -m uvicorn main:app --reload --host 127.0.0.1 --port 8000
```

Open API documentation:

```text
http://127.0.0.1:8000/docs
```

## Quick API Check

Create a user:

```bash
curl -X POST "http://127.0.0.1:8000/api/auth/signup" \
  -H "Content-Type: application/json" \
  -d "{\"username\":\"andreydev\",\"email\":\"andreydev@example.com\",\"password\":\"password123\"}"
```

Read user profile:

```bash
curl "http://127.0.0.1:8000/api/user_option/username?username=andreydev"
```

Expected profile response includes:

```json
{
  "username": "andreydev",
  "email": "andreydev@example.com",
  "role": "admin",
  "photos_uploaded": 0
}
```

## Notes

- The first registered user becomes `admin`.
- Login requires `confirmed=true` for the user.
- Photo upload and transformations require valid Cloudinary credentials.
- This repository is optimized for local portfolio review. A paid cloud deployment is not required to evaluate the backend.

## Deployment

Koyeb deployment notes are available in [DEPLOYMENT.md](DEPLOYMENT.md).
