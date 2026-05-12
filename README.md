# DeepFocus Landing Page — GitHub Pages Site

This directory contains a minimalist, premium, and SEO-optimized landing page for **DeepFocus**. It is designed to act as your official GitHub Pages site, allowing users to discover DeepFocus, play with an interactive dashboard preview, and directly download the latest Windows installer build fetched dynamically via the GitHub Releases API.

## 📁 Directory Structure
- `index.html`: The semantic structure of the site, complete with SEO keywords, Open Graph metadata, and structured JSON-LD schema markup.
- `styles.css`: The stylesheet. Employs a deep-space dark theme, custom responsive grids, glassmorphism filters, ambient glowing keyframe animations, and simulated interface styling.
- `app.js`: Connects to your GitHub repository's Release API to extract installer links, sizes, and downloads. Includes a simulated local focus timer widgets, and interactive FAQ accordions.

---

## 🚀 How It Works

1. **Dynamic Releases**: On page load, `app.js` queries `https://api.github.com/repos/Hello-Mirage/deepfocus/releases/latest`.
   - It updates all version labels (e.g. `v1.0.0`) and dates on the landing page.
   - It searches the release assets for Windows installer executables (`.exe` or `.msi`) and automatically maps them to the main **Download** CTA.
   - It renders a list of all downloadable files (with file size and download counters) so users can download specific files.
   - **Offline Fallback**: If the API rate limit is hit, or the repository has no releases yet, the page loads a mock release list and gracefully falls back to your repository's public releases page.
2. **Interactive Mock Timer**: Users can click **Start Focus** on the web replica app inside the hero section. The timer will start counting down from 25:00 and active states will glow, illustrating the real app's core feature right on their screens.

---

## 🛠️ Customization & Local Testing

### 1. Change Your GitHub Repository
To link the site to a different repository, simply open `app.js` and edit the configuration object at the top:
```javascript
const CONFIG = {
    githubRepo: 'Hello-Mirage/deepfocus', // Replace with 'YOUR_USERNAME/YOUR_REPO'
    defaultTimerDuration: 25 * 60,       // Default simulated duration (seconds)
};
```

### 2. Test Locally
You can test the site locally by opening `index.html` directly in any browser. For optimal API loading, run a local web server in this directory:
- **Python**: `python -m http.server 8000`
- **Node.js (npx)**: `npx live-server` or `npx serve`

---

## 🌐 Deploying to GitHub Pages

To host this site for free on GitHub Pages:

### Option A: From a subfolder on your `main` branch (e.g. using a GitHub action)
Create a workflow `.github/workflows/static.yml` to automatically deploy the `githubsite` subfolder on pushes to `main`.

### Option B: Deploying via a custom branch (Recommended for subfolders)
You can push the contents of this folder directly to a branch called `gh-pages`. Here is how you can do it via terminal in the workspace root:

1. Initialize git in this folder or verify it exists:
   ```bash
   cd githubsite
   git init
   ```
2. Commit and push to a separate repository or as a `gh-pages` branch on your main repository:
   ```bash
   git add .
   git commit -m "Deploy DeepFocus landing site"
   git remote add origin https://github.com/Hello-Mirage/deepfocus.git
   git push -u origin main:gh-pages --force
   ```
3. Go to your **GitHub Repository Settings** -> **Pages**:
   - Under **Build and deployment**, set the Source to **Deploy from a branch**.
   - Select the branch `gh-pages` and folder `/ (root)`.
   - Click Save. Your landing page will be live at `https://Hello-Mirage.github.io/deepfocus/`!
