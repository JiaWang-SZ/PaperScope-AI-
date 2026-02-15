<div align="center">
<img width="1200" height="475" alt="GHBanner" src="https://github.com/user-attachments/assets/0aa67016-6eaf-458a-adb2-6e31a0763ed6" />
</div>

# Run and deploy your AI Studio app

This contains everything you need to run your app locally.

View your app in AI Studio: https://ai.studio/apps/drive/1m2KdlZuuyW-A6rc63bxpq9mwJ9DBG0Wf

**Live Demo:** https://jiawang-sz.github.io/LabPage/

## Run Locally

**Prerequisites:**  Node.js


1. Install dependencies:
   `npm install`
2. Set the `GEMINI_API_KEY` in [.env.local](.env.local) to your Gemini API key
3. Run the app:
   `npm run dev`

## GitHub Pages Deployment

This repository is configured to automatically deploy to GitHub Pages when changes are pushed to the `main` branch.

### Deployment Process

1. The GitHub Actions workflow (`.github/workflows/deploy-pages.yml`) automatically triggers on push to `main`
2. It builds the Vite application with the correct base path (`/LabPage/`)
3. The built files are uploaded and deployed to GitHub Pages

### Manual Deployment

To manually trigger a deployment:
1. Go to the Actions tab in GitHub
2. Select the "Deploy to GitHub Pages" workflow
3. Click "Run workflow" and select the `main` branch

### GitHub Pages Settings

Ensure that in your repository settings:
- Go to Settings → Pages
- Source should be set to "GitHub Actions"
- The site will be published at: https://jiawang-sz.github.io/LabPage/
