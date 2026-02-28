# sfl-multi-agents-admin

Standalone admin dashboard for Stayforlong multi-agent AI. Plain HTML/JS — no build step required.

## Features

- **Conversations tab** — live list with filters (status, language), search by user ID, full message thread view with agent labels
- **Agents tab** — view and edit specialist agent system instructions (requires `GET/PATCH /admin/api/agents` on the backend)
- **Stats bar** — total conversations, started today, unique users, active now (auto-refreshes every 30s)

## Usage

Open `index.html` directly in a browser or serve it from any static host. Pass the backend URL and API key as query params:

```
file:///path/to/index.html?backend=http://localhost:8000&key=YOUR_KEY
https://your-admin.netlify.app/?backend=https://your-adk.railway.app&key=YOUR_KEY
```

### Query params

| Param | Description |
|---|---|
| `backend` | URL of `sfl-multi-agents-adk` (default: same origin) |
| `key` | Admin API key (sent as `Authorization: Bearer KEY`) |

## Deploy

Any static host works — no server needed:

```bash
# Netlify drag & drop
# Vercel: vercel --prod
# S3: aws s3 cp index.html s3://your-bucket/
# Nginx: copy index.html to /var/www/html/admin/
```

## Agents tab — backend requirements

The Agents tab calls these endpoints on `sfl-multi-agents-adk`:

| Method | Path | Description |
|---|---|---|
| `GET` | `/admin/api/agents` | List all agents with name, model, instruction, tools |
| `PATCH` | `/admin/api/agents/{name}` | Update agent instruction |

These endpoints need to be added to `sfl-multi-agents-adk/admin/router.py`. The Conversations tab works with the existing API.

## Related repos

- **sfl-multi-agents-adk** — FastAPI + Vertex AI multi-agent backend
- **sfl-multi-agents-chat** — GTM-injectable chat widget
