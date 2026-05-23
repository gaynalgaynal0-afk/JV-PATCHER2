# ⚡ JV Patcher

Instant MP4 → 60 FPS atom patcher. No FFmpeg. No re-encoding. Patches complete in under 1 second.

---

## 📁 Project Structure

```
jv-patcher/
├── public/
│   ├── index.html      ← Main app UI
│   ├── patcher.js      ← Pure-JS MP4 atom patching logic
│   ├── _headers        ← Cloudflare Pages / Netlify headers
│   └── _redirects      ← SPA routing fallback
├── wrangler.toml       ← Cloudflare Pages config
├── netlify.toml        ← Netlify config
├── package.json
└── README.md
```

---

## 🚀 Deploy to Cloudflare Pages

### Option A — Dashboard (easiest)
1. Go to [Cloudflare Dashboard](https://dash.cloudflare.com) → **Pages** → **Create a project**
2. Connect your GitHub repo **or** choose **Direct Upload**
3. For Direct Upload: drag the entire `public/` folder
4. Set **Build output directory** → `public`
5. Leave **Build command** empty (no build step needed)
6. Click **Save and Deploy**

### Option B — Wrangler CLI
```bash
npm install
npm run deploy:cf
```
> First time: `npx wrangler login` to authenticate

---

## 🚀 Deploy to Netlify

### Option A — Dashboard (drag & drop)
1. Go to [Netlify](https://app.netlify.com) → **Add new site** → **Deploy manually**
2. Drag the `public/` folder into the deploy dropzone
3. Done — your site is live instantly

### Option B — Netlify CLI
```bash
npm install
npm run deploy:netlify
```
> First time: `npx netlify-cli login` to authenticate

### Option C — GitHub integration
1. Push this repo to GitHub
2. In Netlify dashboard: **Import from Git**
3. Set **Publish directory** → `public`
4. Leave **Build command** empty
5. Deploy

---

## 💻 Local Development

```bash
npm install
npm run dev
# Open http://localhost:3000
```

---

## ⚙️ How It Works

The patcher reads the MP4 file entirely in the browser using the [File API](https://developer.mozilla.org/en-US/docs/Web/API/File/arrayBuffer), then:

1. **Finds** the `trak` box for the video track
2. **Reads** `mdhd` timescale (e.g. `90000`)
3. **Calculates** new `sample_delta` = `timescale / 60` (e.g. `1500`)
4. **Writes** the new delta into every `stts` entry
5. Outputs a `Blob` for instant download

No server, no FFmpeg, no re-encoding. The video data is untouched — only the timing metadata changes.

---

## 📄 License

MIT — free to use, fork, and deploy.
