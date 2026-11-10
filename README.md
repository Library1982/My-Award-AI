# My Award AI

Bilingual Arabic/English award-jury digital representative. This repository contains **code only**. Do not commit personal media, award submissions, or secrets.

## Local setup (Windows)
```bat
py -m venv .venv
.venv\Scripts\python -m pip install -r requirements.txt
copy .env.example .env
```
Edit `.env` privately. Add your own OpenAI API key and a strong, unique jury access token. Place the award application at `private/award.pdf` and optionally your JPEG portrait at `private/avatar.jpg`. Do **not** commit these files.

```bat
.venv\Scripts\python -m uvicorn main:app --reload --port 8000 --env-file .env
```
Visit http://127.0.0.1:8000 . Enter the `JURY_ACCESS_TOKEN` value, not the OpenAI API key.

## Render deployment
Create a Render Web Service from this repository, Python environment, build command `pip install -r requirements.txt`, start command `uvicorn main:app --host 0.0.0.0 --port $PORT`. Set `OPENAI_API_KEY`, `JURY_ACCESS_TOKEN`, `OPENAI_MODEL` in Render Environment. **The service will not answer award-specific questions until you securely provision `private/award.pdf` on the server.** A public GitHub repository is not an appropriate location for the confidential PDF. Render's ephemeral filesystem means uploaded documents can disappear after restart; use private persistent storage for production.

The browser microphone requires permission and HTTPS (Render supplies HTTPS). Enterprise-managed devices can still block microphone access.

This is a disclosed AI representative, not a live person. Voice playback uses browser speech synthesis, not cloned speech or realistic lip synchronization.
