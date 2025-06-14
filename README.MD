# Telegram Bot Template

This repository provides a starting point for building Telegram bots using [aiogram v3](https://github.com/aiogram/aiogram/tree/dev-3.x).
It includes optional integration with SQLAlchemy and Alembic and comes with a Docker setup for local development.

## Features
- Basic project layout with example handlers
- Optional PostgreSQL configuration via SQLAlchemy 2.0
- Alembic migrations for database schema management
- Docker configuration for quick startup

## Getting Started
1. Copy `.env.dist` to `.env` and fill in your bot token and other settings.
2. Add your own handlers inside the `tgbot/handlers` package.

### Running with Docker
1. Install [Docker](https://docs.docker.com/get-docker/) and [docker-compose](https://docs.docker.com/compose/).
2. Start the project:
   ```bash
   docker-compose up
   ```

### Running locally
1. Create a virtual environment and activate it:
   ```bash
   python3 -m venv .venv
   source .venv/bin/activate
   ```
2. Install dependencies:
   ```bash
   pip install -r requirements.txt --pre
   ```
3. Launch the bot:
   ```bash
   python3 bot.py
   ```

## Registering Handlers
Create a new module in `tgbot/handlers` and define a router:
```python
from aiogram import Router

my_router = Router()

@my_router.message(commands=["start"])
async def start_cmd(message):
    await message.reply("Hello from the bot!")
```
Add your router to `routers_list` inside `tgbot/handlers/__init__.py` so the bot can load it.

## Database and Migrations
1. Fill out database settings in `.env` if you plan to use PostgreSQL.
2. Uncomment the `api`, `pg_database` and `volumes` sections in `docker-compose.yml` and the database configuration lines in `config.py`.
3. Rebuild and start the containers:
   ```bash
   docker-compose up --build
   ```
4. Apply migrations:
   ```bash
   docker-compose exec api alembic upgrade head
   ```

## Additional Resources
- [aiogram v3 guide](https://mastergroosha.github.io/aiogram-3-guide)
