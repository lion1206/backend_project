# Django Users API (Docker + Render)

## Локальный запуск
```bash
docker build -t django-backend .
docker run -d -p 8000:8000 django-backend
# Открой http://127.0.0.1:8000/api/users/
```

## Деплой на Render
1) Загрузите содержимое этой папки в новый публичный репозиторий GitHub.
2) Войдите на https://render.com → New → Web Service.
3) Подключите репозиторий.
4) Настройки:
   - Environment: **Docker**
   - Branch: *ваша ветка (обычно main)*
   - Port: **8000**
5) Render соберёт Docker-образ и запустит контейнер.
6) Проверьте:
   - GET `https://<service>.onrender.com/api/users/`
   - POST `https://<service>.onrender.com/api/users/register/` c JSON:
     ```json
     { "username": "test", "password": "12345", "email": "test@mail.com" }
     ```

## Структура
```
backend_project/
├─ Dockerfile
├─ requirements.txt
├─ manage.py
├─ .gitignore
├─ README.md
├─ backend/
│  ├─ __init__.py
│  ├─ settings.py
│  ├─ urls.py
│  ├─ wsgi.py
│  └─ asgi.py
└─ users_api/
   ├─ __init__.py
   ├─ admin.py
   ├─ apps.py
   ├─ models.py
   ├─ serializers.py
   ├─ views.py
   ├─ urls.py
   └─ migrations/
      └─ __init__.py
```

## Примечание
- Для простоты используется SQLite. Для продакшена лучше Postgres.
- Имя пакета настроек — `backend`, **не `app`**.
