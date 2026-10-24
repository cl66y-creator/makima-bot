# Free AI Chatbot (OpenRouter + Vercel)

A simple chatbot that uses free OpenRouter models and runs on Vercel's free Hobby plan.

## Files

- `index.html` – the chat page
- `api/chat.js` – serverless function that calls OpenRouter (keeps your key secret)
- `package.json` – tells Vercel to treat the function as an ES module

## 0. Add Makima's profile picture

Save your picture as `avatar.png` in the project root (next to `index.html`). It is used as the bot's profile picture in the header, on every bot message, and as the browser tab icon. Until you add it, a pink "M" is shown instead.

## 1. Get an OpenRouter API key

1. Sign up at https://openrouter.ai
2. Go to **Keys** and create a new key (starts with `sk-or-...`)
3. No credit card is needed for free models

## 2. Pick a free model

Free models have `:free` at the end of their ID. Browse them at https://openrouter.ai/models?q=free

The default in `api/chat.js` is `meta-llama/llama-3.3-70b-instruct:free`. Free model lists change over time, so if you get a "model not found" error, pick a current one and set it via the `OPENROUTER_MODEL` environment variable (below).

Free models have rate limits (a limited number of requests per minute and per day), which is the trade-off for zero cost.

## 3. Deploy to Vercel (free)

### Option A: Vercel dashboard (easiest)

1. Push this folder to a GitHub repository.
2. Go to https://vercel.com/new and import the repo.
3. Before clicking Deploy, open **Environment Variables** and add:
   - `OPENROUTER_API_KEY` = your key
   - `OPENROUTER_MODEL` = a `:free` model ID (optional)
4. Click **Deploy**.

### Option B: Vercel CLI

```bash
npm i -g vercel
cd openrouter-chatbot
vercel
vercel env add OPENROUTER_API_KEY
vercel --prod
```

## Run locally (optional)

```bash
npm i -g vercel
vercel dev
```

Create a `.env.local` file with `OPENROUTER_API_KEY=sk-or-...` first.

## Important

- Never put your API key in `index.html` or commit it to GitHub. It belongs only in Vercel's environment variables.
- Anyone with your site URL can use your free quota. If you share it widely, consider adding a simple password or rate limit.
