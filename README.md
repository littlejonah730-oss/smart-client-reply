# Deploying Smart Client Reply

This folder is ready to deploy as-is on **Vercel** (free, no credit card required for the hobby tier).

## 1. Get an Anthropic API key
1. Go to https://console.anthropic.com
2. Sign up / log in, add billing (usage is pay-per-token — for this kind of app it's typically a few cents to a few dollars a month depending on volume)
3. Create an API key under **API Keys** — copy it somewhere safe. You will paste it into Vercel, never into this code.

## 2. Put this folder on GitHub
1. Create a new repo on https://github.com (e.g. `smart-client-reply`)
2. Upload these three items into it: `index.html`, the `api` folder (with `generate.js` inside), and this `README.md`

## 3. Deploy on Vercel
1. Go to https://vercel.com and sign up (you can use your GitHub account to log in)
2. Click **Add New → Project**, then import the repo you just created
3. Framework preset: choose **Other** (it's a static site + one serverless function, no build step needed)
4. Before clicking Deploy, open **Environment Variables** and add:
   - Name: `ANTHROPIC_API_KEY`
   - Value: (the key you copied in step 1)
5. Click **Deploy**

Vercel gives you a live URL immediately (like `smart-client-reply.vercel.app`), and you can attach your own domain later for free in the project's **Domains** tab.

## How it works
- `index.html` is the whole app — customers, templates, history, insights all live in your browser's local storage (private to your device/browser, never sent anywhere).
- When you click "Generate Reply," the page calls `/api/generate` on your own Vercel deployment.
- `api/generate.js` is a small serverless function that adds your API key and forwards the request to Anthropic, then hands the answer back. Your key never touches the browser, so it's never visible to anyone using the site.

## Notes
- Local storage is per-browser. If you use the app on your phone and your laptop, they won't share customer/history data — each device builds its own.
- If you ever want multiple people (e.g. an employee) using the same customer list, that would need a real database instead of local storage — let me know if you want that built out.
