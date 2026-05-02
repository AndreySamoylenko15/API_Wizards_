# Deployment Notes

## Koyeb

Use a GitHub web service with the `main` branch.

Run command:

```bash
uvicorn main:app --host 0.0.0.0 --port ${PORT:-8000}
```

Required environment variables:

```env
POSTGRES_DB=
POSTGRES_USER=
POSTGRES_PASSWORD=
POSTGRES_PORT=5432
POSTGRES_DOMAIN=
SECRET_KEY_JWT=
ALGORITHM=HS256
MAIL_USERNAME=
MAIL_PASSWORD=
MAIL_FROM=
MAIL_PORT=
MAIL_SERVER=
REDIS_DOMAIN=
REDIS_PORT=6379
REDIS_PASSWORD=
cloud_name=
api_key=
api_secret=
```

After the database variables are configured, run migrations once:

```bash
python -m alembic upgrade head
```

The API documentation should be available at:

```text
https://<your-koyeb-domain>/docs
```
