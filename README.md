<div align="center">

<img src="docs/assets/seal-1.png" alt="Supreme Student Advisory Council seal" width="110" />

# Supreme Student Advisory Council — IIUI

**Official registration platform for the Supreme Student Advisory Council**
International Islamic University, Islamabad (IIUI)

A full-stack, bilingual (English / العربية) web application for registering students,
managing councils and competitions, and administering submissions from a single
secure dashboard.

[![Node.js](https://img.shields.io/badge/Node.js-18%2B-339933?logo=node.js&logoColor=white)](https://nodejs.org/)
[![Express](https://img.shields.io/badge/Express-REST%20API-000000?logo=express&logoColor=white)](https://expressjs.com/)
[![SQLite](https://img.shields.io/badge/SQLite-better--sqlite3-003B57?logo=sqlite&logoColor=white)](https://www.sqlite.org/)
[![Deploy](https://img.shields.io/badge/Deploy-Render%20%7C%20Docker%20%7C%20GitHub%20Pages-219EBC)](#-deployment)
[![i18n](https://img.shields.io/badge/i18n-EN%20%2F%20AR%20(RTL)-FB8500)](#-features)

</div>

---

## 📖 Overview

This project powers the online presence and registration workflow of the Supreme
Student Advisory Council at IIUI. Students can register and enter competitions from
any device, while administrators review every submission from a central, protected
dashboard.

The same codebase runs in **two modes** with no code changes:

| Mode | Hosting | Where data lives |
|------|---------|------------------|
| **Static** | GitHub Pages (free) | Each visitor's own browser |
| **Full** | Render / Railway / Docker | Central SQLite database — admin sees every submission from every device |

The front-end automatically uses the back-end when one is present and falls back to
browser storage when it isn't.

---

## ✨ Features

- 🌐 **Bilingual UI** — full English / Arabic support with right-to-left (RTL) layout.
- 📝 **Student registration** — simple, validated sign-up for councils and competitions.
- 🔐 **Secure admin panel** — token-based (JWT) authentication with rate limiting.
- 📊 **Central dashboard** — totals per council and per faculty, with record management.
- 🏆 **Competitions module** — manage competitions and their registrations.
- 🧩 **Portable deploys** — one codebase runs on Render, Railway, Fly.io, Docker, or GitHub Pages.
- 🗄️ **Durable storage** — SQLite via `better-sqlite3`, with PostgreSQL support for serverless hosts.

---

## 🛠️ Tech stack

- **Front-end:** HTML, CSS, vanilla JavaScript (bilingual, RTL-aware).
- **Back-end:** Node.js + Express REST API with token-based admin authentication.
- **Database:** SQLite (`better-sqlite3`) for the full server; `pg` (PostgreSQL) adapters for serverless deploys (Vercel / Netlify).

---

## 📁 Project structure

```
.
├── server.js            # Express app: serves the API + the front-end
├── db.js                # SQLite database layer
├── package.json
├── .env.example         # copy to .env and fill in
├── Dockerfile           # container deploy (any host)
├── render.yaml          # one-click deploy to Render.com
├── vercel.json          # Vercel serverless config
├── netlify.toml         # Netlify serverless config
├── api/                 # serverless API handlers (Vercel)
├── netlify/functions/   # serverless API handlers (Netlify)
├── public/              # the front-end (served by the Node server)
│   ├── index.html
│   ├── css/styles.css
│   ├── js/app.js
│   └── assets/          # logos, hero background, president photo
└── docs/                # static copy for GitHub Pages
```

---

## 🔌 API

| Method | Route                  | Access | Purpose                        |
|--------|------------------------|--------|--------------------------------|
| POST   | `/api/register`        | public | Submit a registration          |
| POST   | `/api/admin/login`     | public | Exchange password for a token  |
| GET    | `/api/registrations`   | admin  | List all registrations         |
| DELETE | `/api/registrations`   | admin  | Delete all registrations       |
| GET    | `/api/health`          | public | Health check                   |

Admin routes require an `Authorization: Bearer <token>` header. The token is issued
by `/api/admin/login` and expires after `TOKEN_TTL` (default 8h).

---

## 🚀 Run it locally

You need [Node.js](https://nodejs.org/) 18 or newer.

```bash
# 1. install dependencies
npm install

# 2. create your config
cp .env.example .env
#    then edit .env and set ADMIN_PASSWORD and JWT_SECRET

# 3. start the server
npm start
```

Open **http://localhost:3000**.

Generate a strong `JWT_SECRET` with:

```bash
node -e "console.log(require('crypto').randomBytes(48).toString('hex'))"
```

### Admin panel

- Click **Admin** in the navbar.
- Log in with the `ADMIN_PASSWORD` you set in `.env`.
- View totals per council and per faculty, and manage records.

---

## ⚙️ Environment variables

| Variable         | Required | Default             | Notes                                          |
|------------------|----------|---------------------|------------------------------------------------|
| `PORT`           | no       | `3000`              | Most hosts set this automatically.             |
| `ADMIN_PASSWORD` | **yes**  | `sac2026`           | The admin login password. **Change it.**       |
| `JWT_SECRET`     | **yes**  | insecure dev        | Long random string used to sign tokens.        |
| `TOKEN_TTL`      | no       | `8h`                | How long an admin stays logged in.             |
| `DB_PATH`        | no       | `./data/council.db` | Point at a persistent disk in production.      |
| `CORS_ORIGIN`    | no       | `*`                 | Restrict which site may call the API.          |

---

## 📦 Deployment

### Option A — GitHub Pages (static, free, no server)

The `docs/` folder is a ready-to-publish copy of the site.

1. Push this repo to GitHub.
2. Open **Settings → Pages**.
3. Under **Build and deployment → Source**, choose **Deploy from a branch**.
4. Set **Branch** to your branch and **Folder** to **`/docs`**, then **Save**.
5. Wait ~1 minute for the link, e.g.
   `https://<your-username>.github.io/Supreme-Student-Advisory-Council/`.

> Static mode stores each browser's registrations locally. To change the admin
> password for static mode, edit `STATIC_ADMIN_PASSWORD` near the top of
> `docs/js/app.js`. For central submissions, use the full deploy below.

### Option B — Render.com (easiest full deploy, free tier)

1. Push this repo to GitHub.
2. On Render: **New → Blueprint**, select this repo. Render reads `render.yaml`
   and provisions the service **plus a 1 GB persistent disk** for the database.
3. Set `ADMIN_PASSWORD` when prompted (`JWT_SECRET` is generated for you).
4. After it deploys, open **Settings → Custom Domains** to attach your domain.

### Option C — Railway / Fly.io / any Node host

- Build command: `npm install`
- Start command: `node server.js`
- Set the environment variables from the table above.
- Attach a **persistent volume** and set `DB_PATH` to a path on it (e.g.
  `/data/council.db`) so registrations survive restarts.

### Option D — Docker (VPS or any container host)

```bash
docker build -t ssac .
docker run -d -p 80:3000 \
  -e ADMIN_PASSWORD='your-strong-password' \
  -e JWT_SECRET='your-long-random-secret' \
  -e DB_PATH='/data/council.db' \
  -v ssac-data:/data \
  ssac
```

Then point your domain's `A` record at the server's IP address.

---

## 🔒 Security

- Always set a strong `ADMIN_PASSWORD` and a random `JWT_SECRET` in production.
- The login endpoint is rate-limited (20 attempts / 15 min) and registration is
  rate-limited (10 / min) to discourage abuse.
- Serve the site over HTTPS (Render, Railway, Fly and most hosts provide this
  automatically once a domain is attached).

---

## 🎨 Color palette

| Token  | Value     | Preview |
|--------|-----------|---------|
| Navy   | `#023047` | ![navy](https://img.shields.io/badge/-023047-023047) |
| Teal   | `#219EBC` | ![teal](https://img.shields.io/badge/-219EBC-219EBC) |
| Sky    | `#8ECAE6` | ![sky](https://img.shields.io/badge/-8ECAE6-8ECAE6) |
| Amber  | `#FFB703` | ![amber](https://img.shields.io/badge/-FFB703-FFB703) |
| Orange | `#FB8500` | ![orange](https://img.shields.io/badge/-FB8500-FB8500) |
| Paper  | `#F5FAFC` | ![paper](https://img.shields.io/badge/-F5FAFC-F5FAFC) |

---

<div align="center">

Built for the **Supreme Student Advisory Council**, International Islamic University, Islamabad.

</div>
