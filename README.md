<div align="center">

# 🎓 Thesis Scheduling System

**Web-Based Thesis Scheduling System with Expertise-Based Panel Assignment**

BSIT Capstone Project · College of Computing and Information Sciences (CCIS) · Caraga State University

![Nuxt](https://img.shields.io/badge/Nuxt-00DC82?style=for-the-badge&logo=nuxt&logoColor=white)
![Supabase](https://img.shields.io/badge/Supabase-3FCF8E?style=for-the-badge&logo=supabase&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=for-the-badge&logo=postgresql&logoColor=white)
![Google Gemini](https://img.shields.io/badge/Google%20Gemini-8E75B2?style=for-the-badge&logo=googlegemini&logoColor=white)
![Vercel](https://img.shields.io/badge/Vercel-000000?style=for-the-badge&logo=vercel&logoColor=white)

</div>

---

## 📖 About

This system manages thesis defense schedules and automatically assigns panelists based on their expertise. When a student submits their thesis title, it is matched against embedded panelist expertise using semantic search, and the best-fitting panelists are assigned automatically.

### ✨ Features

- 📅 **Schedule Management** — create and manage thesis defense schedules with conflict checking
- 🧠 **Expertise-Based Panel Assignment** — semantic matching of thesis titles to panelist expertise
- 🔔 **Notifications** — automatic alerts for schedules and panel assignments
- 🔐 **Role-Based Access Control (RBAC)** — separate access for admins and students
- 🤖 **AI Integration** — Google Gemini API for both AI features and text embeddings

---

## 🧰 Tech Stack

| Layer | Technology |
| --- | --- |
| 🖥️ Frontend | Nuxt + Nuxt Content |
| 🗄️ Backend / Database | Supabase (PostgreSQL) |
| 🔑 Authentication | PostgreSQL functions with `pgcrypto` (bcrypt) |
| 🤖 AI / LLM | Google Gemini API |
| 🧬 Embeddings | Google Gemini Embeddings |
| ▲ Hosting | Vercel |

---

## ✅ Prerequisites

Make sure these are installed before you start:

- 🟢 [Node.js](https://nodejs.org/) **v18 or later** (LTS recommended) — check with `node -v`
- 📦 A package manager: **npm** (comes with Node), **pnpm**, **yarn**, or **bun**
- 🌿 [Git](https://git-scm.com/)
- ☁️ A [Supabase](https://supabase.com/) project
- 🔑 A [Google Gemini API key](https://aistudio.google.com/apikey) from Google AI Studio
- ▲ A [Vercel](https://vercel.com/) account (for deployment)

---

## 🚀 Getting Started

### 1️⃣ Clone the repository

```bash
git clone <your-repo-url>
cd <your-project-folder>
```

### 2️⃣ Install dependencies

Pick **one** package manager and stick with it:

```bash
# npm
npm install

# pnpm
pnpm install

# yarn
yarn install

# bun
bun install
```

### 3️⃣ Set up environment variables

Create a `.env` file in the project root:

```env
# Supabase — Project Settings → API
SUPABASE_URL=https://your-project-id.supabase.co
SUPABASE_KEY=your-supabase-anon-key

# Google Gemini — https://aistudio.google.com/apikey
GEMINI_API_KEY=your-gemini-api-key
```

> ⚠️ **Never commit your `.env` file.** Make sure `.env` is listed in `.gitignore`.
> Only use the **anon** key on the client. The **service role** key and the **Gemini API key** must stay on the server (e.g. in `server/api/` routes) and must never be exposed to the browser.

> 💡 Adjust the variable names if your `nuxt.config.ts` expects different ones.

### 4️⃣ Set up the database

1. Open your Supabase project → **SQL Editor**.
2. Run the schema scripts to create the tables (`roles`, `panelist_information`, `panel_expertise`, `panel_assignments`, `thesis_schedule`, `notifications`).
3. Run the functions and triggers scripts (panelist matching, conflict checking, auto-notifications, auth).

> 💡 The database connection string is under **Settings → Database**, not the Database sidebar.

### 5️⃣ Start the development server

```bash
# npm
npm run dev

# pnpm
pnpm dev

# yarn
yarn dev

# bun
bun run dev
```

Open 👉 **http://localhost:3000** in your browser.

---

## 📦 Production

### 🏗️ Build the app

```bash
# npm
npm run build

# pnpm
pnpm build

# yarn
yarn build

# bun
bun run build
```

### 👀 Preview the production build locally

```bash
# npm
npm run preview

# pnpm
pnpm preview

# yarn
yarn preview

# bun
bun run preview
```

---

## ▲ Deploying to Vercel

Vercel auto-detects Nuxt, so no extra config file is needed.

### Option A — Deploy from GitHub (recommended)

1. 📤 Push your project to GitHub.
2. 🔗 Go to [vercel.com/new](https://vercel.com/new) and **Import** your repository.
3. ⚙️ Vercel detects **Nuxt** as the framework preset. Leave the build settings as default:
   - Build Command: `npm run build`
   - Output Directory: *(leave default)*
   - Install Command: `npm install`
4. 🔑 Open **Environment Variables** and add the same values from your `.env`:
   - `SUPABASE_URL`
   - `SUPABASE_KEY`
   - `GEMINI_API_KEY`
5. 🚀 Click **Deploy**.

After this, every push to the `main` branch redeploys automatically, and other branches get preview URLs.

### Option B — Deploy with the Vercel CLI

```bash
# install the CLI
npm install -g vercel

# log in and link the project
vercel login
vercel

# deploy to production
vercel --prod
```

Add environment variables with `vercel env add <NAME>` or in the Vercel dashboard under **Project → Settings → Environment Variables**.

### 🔐 After deploying

- In Supabase, go to **Authentication → URL Configuration** and add your Vercel URL (e.g. `https://your-app.vercel.app`) to **Site URL** / **Redirect URLs** so login redirects work.
- If you change environment variables in Vercel, **redeploy** for the changes to take effect.

> 📘 More details: [Nuxt on Vercel](https://vercel.com/docs/frameworks/nuxt)

---

## 🛠️ Troubleshooting

<details>
<summary>❌ <b>Port 3000 is already in use</b></summary>

**Windows:**

```bash
netstat -ano | findstr :3000
taskkill /PID <PID> /F
```

**macOS / Linux:**

```bash
lsof -i :3000
kill -9 <PID>
```

Or run on another port: `npm run dev -- --port 3001`

</details>

<details>
<summary>❌ <b>Supabase connection errors</b></summary>

- Double-check `SUPABASE_URL` and `SUPABASE_KEY` in `.env`.
- Restart the dev server after editing `.env`.
- Free-plan projects pause after inactivity — open the Supabase dashboard to restore it.

</details>

<details>
<summary>❌ <b>AI requests failing or rate-limited</b></summary>

- Confirm `GEMINI_API_KEY` is valid in Google AI Studio.
- The Gemini free tier has per-minute and per-day request limits. If you get a `429` error, wait and retry.

</details>

<details>
<summary>❌ <b>Works locally but fails on Vercel</b></summary>

- Check that all environment variables are added in Vercel and redeploy.
- Open **Vercel → Project → Deployments → Logs** to see the build or runtime error.
- Make sure your Vercel URL is added in Supabase's **Redirect URLs**.

</details>

<details>
<summary>❌ <b>Dependency or build errors</b></summary>

Delete installed packages and reinstall:

```bash
rm -rf node_modules .nuxt .output
npm install
```

(On Windows PowerShell: `Remove-Item -Recurse -Force node_modules, .nuxt, .output`)

</details>

---

## 📂 Project Structure

```
├── 📁 assets/          # Styles, images, fonts
├── 📁 components/      # Reusable Vue components
├── 📁 content/         # Nuxt Content markdown files
├── 📁 pages/           # App routes
├── 📁 public/          # Static files
├── 📁 server/          # Server API routes
├── 📄 nuxt.config.ts   # Nuxt configuration
├── 📄 package.json
└── 📄 .env             # Environment variables (not committed)
```

---

## 👥 Team

- 👩‍🎓 **Liezle G. Acita** — Researcher
- 👩‍🎓 **Pamela Lyka C. Navarra** — Researcher
- 👨‍💻 **Niko R. Polistico** — Developer

---

## 📚 Resources

- 📘 [Nuxt Documentation](https://nuxt.com/docs)
- 📗 [Nuxt Content Documentation](https://content.nuxt.com)
- 📙 [Supabase Documentation](https://supabase.com/docs)
- 📕 [Gemini API Documentation](https://ai.google.dev/gemini-api/docs)
- 📓 [Vercel Nuxt Documentation](https://vercel.com/docs/frameworks/nuxt)

---

<div align="center">

Made with 💚 at **Caraga State University — CCIS**

</div>
