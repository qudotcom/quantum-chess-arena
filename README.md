# Centrale Quanta — Quantum Chess Arena ♟️⚛️

A multiplayer web platform for **quantum chess**: pieces can be split into superposition, carry complex amplitudes, become entangled, and merge back together. Players register, join a club, play practice games against an AI, and compete in knockout tournaments.

## Features

- **Quantum game engine** (`app/modules/tournament/engine.py`)
  - Every square holds a list of piece states with a complex **amplitude** and **phase**
  - **Split moves** put a piece into superposition across two squares; **merge moves** recombine its branches
  - **Entanglement** tracking, rendered in the UI as matching colour tags
  - Move legality, clone-safe state copies, and game-over detection
- **AI opponent** (`ai.py`) that scores positions by **probability-weighted material** and picks among candidate moves, with difficulty levels
- **Tournaments**: brackets, automatic winner advancement, and chess clocks
- **Accounts & clubs**: registration and login (bcrypt password hashing, session middleware) and a club board

## Architecture

```
app/
├── main.py                 # FastAPI app, middleware, routes
├── core/                   # DB engine (SQLAlchemy/SQLite), security helpers
├── modules/
│   ├── auth/               # users: models, schemas, router
│   ├── club/               # club board
│   └── tournament/         # quantum engine, AI, brackets, match API
├── templates/              # Jinja2 pages (login, club, bracket, game)
└── static/                 # CSS + game client (game_client.js)
```

## Run it

**Docker (recommended)**

```bash
docker build -t quanta .
docker run -p 8000:8000 -e SESSION_SECRET=change-me quanta
```

**Locally** (Python 3.10+)

```bash
pip install -r requirements.txt
mkdir -p data
uvicorn app.main:app --reload
```

Open http://localhost:8000. The SQLite database is created on first start in `data/`.

## Configuration

| Variable | Purpose | Default |
|---|---|---|
| `SESSION_SECRET` | Key used to sign session cookies | dev-only fallback; **set it in production** |

## Tech stack

FastAPI · SQLAlchemy · Jinja2 · passlib/bcrypt · NumPy · Cirq · vanilla JavaScript

## License

MIT
