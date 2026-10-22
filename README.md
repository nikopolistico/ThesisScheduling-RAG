<div align="center">

# 🎓 Thesis Scheduling System

**Web-Based Thesis Scheduling System with Expertise-Based Panel Assignment**

BSIT Capstone Project · College of Computing and Information Sciences (CCIS) · Caraga State University

![Nuxt](https://img.shields.io/badge/Nuxt-00DC82?style=for-the-badge&logo=nuxt&logoColor=white)
![Vue.js](https://img.shields.io/badge/Vue.js-4FC08D?style=for-the-badge&logo=vuedotjs&logoColor=white)
![Supabase](https://img.shields.io/badge/Supabase-3FCF8E?style=for-the-badge&logo=supabase&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=for-the-badge&logo=postgresql&logoColor=white)
![Groq](https://img.shields.io/badge/Groq-F55036?style=for-the-badge&logoColor=white)
![Hugging Face](https://img.shields.io/badge/Hugging%20Face-FFD21E?style=for-the-badge&logo=huggingface&logoColor=black)

</div>

---

## 📖 About

This system manages thesis defense schedules and automatically assigns panelists based on their expertise. When a student submits their thesis title, it is matched against embedded panelist expertise using semantic search, and the best-fitting panelists are assigned automatically.

### ✨ Features

- 📅 **Schedule Management** — create and manage thesis defense schedules with conflict checking
- 🧠 **Expertise-Based Panel Assignment** — semantic matching of thesis titles to panelist expertise
- 🔔 **Notifications** — automatic alerts for schedules and panel assignments
- 🔐 **Role-Based Access Control (RBAC)** — separate access for admins, panelists, and students
- 🤖 **AI Integration** — Groq (`llama-3.3-70b-versatile`) for AI features, Hugging Face for embeddings

---

## 🧰 Tech Stack

| Layer | Technology |
| --- | --- |
| 🖥️ Frontend | Nuxt + Nuxt Content |
| 🗄️ Backend / Database | Supabase (PostgreSQL) |
| 🔑 Authentication | PostgreSQL functions with `pgcrypto` (bcrypt) |
| 🤖 AI / LLM | Groq API (OpenAI-compatible SDK) |
| 🧬 Embeddings | Hugging Face Inference API |

---

## ✅ Prerequisites

Make sure these are installed before you start:

- 🟢 [Node.js](https://nodejs.org/) **v18 or later** (LTS recommended) — check with `node -v`
- 📦 A package manager: **npm** (comes with Node), **pnpm**, **yarn**, or **bun**
- 🌿 [Git](https://git-scm.com/)
- ☁️ A [Supabase](https://supabase.com/) project
- 🔑 API keys for [Groq](https://console.groq.com/) and [Hugging Face](https://huggingface.co/settings/tokens)

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

# Groq — https://console.groq.com/keys
GROQ_API_KEY=your-groq-api-key

# Hugging Face — https://huggingface.co/settings/tokens
HF_API_TOKEN=your-huggingface-token
```

> ⚠️ **Never commit your `.env` file.** Make sure `.env` is listed in `.gitignore`.
> Only use the **anon** key on the client. The **service role** key must stay on the server and must never be shared publicly.

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

### 🌐 Deploy

See the [Nuxt deployment documentation](https://nuxt.com/docs/getting-started/deployment) for hosting options. Remember to add your environment variables to your hosting provider's settings.

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

- Confirm `GROQ_API_KEY` is valid.
- Groq's free tier has limits (around 30 requests/minute and 1,000/day). Wait and retry, or switch to a backup provider such as OpenRouter.

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
- 📕 [Groq API Documentation](https://console.groq.com/docs)

---

<div align="center">

Made with 💚 at **Caraga State University — CCIS**

</div>
