# Task Manager REST API

FastAPI + SQLAlchemy backend with JWT authentication, role-based access, filtering and pagination.

## Features
- Register / login (JWT bearer tokens, PBKDF2-hashed passwords)
- Task CRUD with category, due date, completed flag
- Filtering (`?completed=true&category=work`) and pagination (`?skip=0&limit=20`)
- Users only see their own tasks; admins can see all (`?all_users=true`, `GET /auth/users`)
- SQLite by default, PostgreSQL via `DATABASE_URL`
- Docker + docker-compose, GitHub Actions CI, pytest suite

## Run it
```bash
./run.sh          # Linux/macOS      |   run.bat on Windows
```
Then open http://127.0.0.1:8000/docs (interactive Swagger UI). Click **Authorize** after logging in.

### With Docker + PostgreSQL
```bash
docker compose up --build
```

### Tests
```bash
pip install -r requirements.txt
pytest -q
```

## Make an admin
Set `ADMIN_EMAIL=you@example.com` before starting, then register with that email.

## Project layout
```
app/
  main.py        app + lifespan
  database.py    engine / session
  models.py      User, Task
  schemas.py     Pydantic models
  security.py    hashing + JWT
  deps.py        auth dependencies
  routers/       auth.py, tasks.py
tests/           pytest suite
```

## Ideas to extend (good interview talking points)
Alembic migrations, refresh tokens, rate limiting, task sharing between users, deploy on Render/Railway.

## Run in VS Code
1. Unzip, then **File > Open Folder** and select this folder.
2. Open a terminal (**Terminal > New Terminal**) and create the environment:
   - Windows: `python -m venv .venv` then `.venv\Scripts\activate`
   - Mac/Linux: `python3 -m venv .venv` then `source .venv/bin/activate`
3. Install: `pip install -r requirements.txt`
4. If VS Code asks, select the `.venv` interpreter (Ctrl+Shift+P > "Python: Select Interpreter").
5. Run: `uvicorn app.main:app --reload` (or press F5) and open http://127.0.0.1:8000/docs.
6. Tests: open the Testing panel (flask icon) or run `pytest -q`.
