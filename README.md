# 🧠 Vibecode Editor – AI-Powered Web IDE

![Vibecode Editor Thumbnail](public/vibe-code-editor-thumbnaail.svg)

**Vibecode Editor** is a blazing-fast, AI-integrated web IDE built entirely in the browser using **Next.js App Router**, **WebContainers**, **Monaco Editor**, and **local LLMs via Ollama**. It offers real-time code execution, an AI-powered chat assistant, and support for multiple tech stacks — all wrapped in a stunning developer-first UI.

---

## 🚀 Features

- 🔐 **OAuth Login with NextAuth** – Supports Google & GitHub login.
- 🎨 **Modern UI** – Built with TailwindCSS & ShadCN UI.
- 🌗 **Dark/Light Mode** – Seamlessly toggle between themes.
- 🧱 **Project Templates** – Choose from React, Next.js, Express, Hono, Vue, or Angular.
- 🗂️ **Custom File Explorer** – Create, rename, delete, and manage files/folders easily.
- 🖊️ **Enhanced Monaco Editor** – Syntax highlighting, formatting, keybindings, and AI autocomplete.
- 💡 **AI Suggestions with Ollama** – Local models give you code completion on `Ctrl + Space` or double `Enter`. Accept with `Tab`.
- ⚙️ **WebContainers Integration** – Instantly run frontend/backend apps right in the browser.
- 💻 **Terminal with xterm.js** – Fully interactive embedded terminal experience.
- 🤖 **AI Chat Assistant** – Share files with the AI and get help, refactors, or explanations.

---

## 🧱 Tech Stack

| Layer         | Technology                                   |
|---------------|----------------------------------------------|
| Framework     | Next.js 15 (App Router)                      |
| Styling       | TailwindCSS, ShadCN UI                       |
| Language      | TypeScript                                   |
| Auth          | NextAuth (Google + GitHub OAuth)             |
| Editor        | Monaco Editor                                |
| AI Suggestion | Ollama (LLMs running locally via Docker)     |
| Runtime       | WebContainers                                |
| Terminal      | xterm.js                                     |
| Database      | MongoDB (via DATABASE_URL)                   |

---

## 🛠️ Getting Started

### 1. Clone the Repo

```bash
git clone https://github.com/Light-Ak/Web-IDE.git
cd vibecode-editor
````

### 2. Install Dependencies

```bash
npm install
```

### 3. Set Up Environment Variables

Create a `.env.local` file using the template:

```bash
cp .env.example .env.local
```

Then, fill in your credentials:

```env
AUTH_SECRET=your_auth_secret
AUTH_GOOGLE_ID=your_google_client_id
AUTH_GOOGLE_SECRET=your_google_secret
AUTH_GITHUB_ID=your_github_client_id
AUTH_GITHUB_SECRET=your_github_secret
DATABASE_URL=your_mongodb_connection_string
NEXTAUTH_URL=http://localhost:3000
OLLAMA_MODEL=qwen2.5-coder:1.5b
```

### 4. Start Local Ollama Model

Make sure [Ollama](https://ollama.com/) and Docker are installed, then run:

```bash
ollama run qwen2.5-coder:1.5b
```

Or use your preferred model that supports code generation.

### 5. Run the Development Server

```bash
npm run dev
```

Visit `http://localhost:3000` in your browser.

---

## 🚀 Deployment Guide

To deploy Vibecode Editor to a provider like Vercel, Railway, or Render:

1. **Database:** Ensure your MongoDB Atlas cluster allows connections from your hosting provider (whitelist `0.0.0.0/0` under Network Access if using serverless platforms like Vercel).
2. **OAuth Callbacks:** Go to your Google Cloud Console and GitHub Developer Settings, and add your production domain to the authorized redirect URIs.
   - Example: `https://yourdomain.com/api/auth/callback/google`
3. **Environment Variables:** Add all variables from your `.env.local` to your hosting provider's environment settings. **Important:** Change `NEXTAUTH_URL` to your production domain!
4. **AI/Ollama Backend:** 
   - Since the Next.js backend runs on the cloud, it cannot access `localhost` on the end-user's computer. 
   - To use AI in production, you must host Ollama on a VPS with a public IP and set the `OLLAMA_BASE_URL` environment variable to point to your VPS (e.g., `http://your-vps-ip:11434`).
   - *Warning: Be sure to secure your hosted Ollama instance (e.g., via a reverse proxy like Nginx with basic auth or IP whitelisting) to prevent unauthorized usage.*
5. **WebContainer Headers:** The `next.config.mjs` file already includes the required `Cross-Origin-Embedder-Policy` and `Cross-Origin-Opener-Policy` headers needed for WebContainers to function in production.

---

## ❓ Troubleshooting

- **WebContainers won't start:** Make sure your browser supports `SharedArrayBuffer`. You must access the deployed site via `https://`, and ensure you aren't using an aggressive ad-blocker that strips Cross-Origin headers.
- **AI responds with "Failed to fetch":** Ensure your Ollama server is running and the model (`qwen2.5-coder:1.5b`) is installed. Check that the `OLLAMA_BASE_URL` is accessible from your deployed environment.


---

## 🎯 Keyboard Shortcuts

* `Ctrl + Space` or `Double Enter`: Trigger AI suggestions
* `Tab`: Accept AI suggestion
* `/`: Open Command Palette (if implemented)

---



---

## 📄 License

This project is licensed under the [MIT License](LICENSE).

---

## 🙏 Acknowledgements

* [Monaco Editor](https://microsoft.github.io/monaco-editor/)
* [Ollama](https://ollama.com/) – for offline LLMs
* [WebContainers](https://webcontainers.io/)
* [xterm.js](https://xtermjs.org/)
* [NextAuth.js](https://next-auth.js.org/)


