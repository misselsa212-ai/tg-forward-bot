# Telegram Forward Bot

Railway-ready Telegram worker for forwarding media between channels and running the downloader and scraper flows.

## Deploy on Railway

1. Create a Railway project from this GitHub repository.
2. Add the variables below in the service settings.
3. Deploy. Railway runs `python main.py` as a worker.

Required variables:

- `BOT_TOKEN`: Telegram Bot API token.
- `ADMIN_IDS`: comma-separated Telegram user IDs, for example `123456789,987654321`.
- `FERNET_KEY`: stable Fernet key for encrypted stored credentials. Generate one with `python -c "from cryptography.fernet import Fernet; print(Fernet.generate_key().decode())"`.

Optional variables:

- `API_ID` and `API_HASH`: default Telegram API credentials.
- `RAPIDAPI_KEY`: enables the RapidAPI downloader backend.
- `PROXY_URL` and `PREMIUM_PROXY`: proxy configuration.

Attach a Railway volume if SQLite state, Telegram sessions, and downloaded records must survive redeploys. Mount it at `/app/tg forward bot` or update the application paths for the chosen mount point.

Never commit `.env`, Telegram session files, databases, logs, or downloaded media.