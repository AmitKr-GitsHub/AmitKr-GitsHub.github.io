# Quarto Portfolio (GitHub Pages)

If your site shows a GitHub Pages error like **"refresh repository"**, it usually means Pages is not configured to deploy built HTML yet.

## Fix (one-time)

1. Push this repository to GitHub.
2. Go to **Settings → Pages**.
3. Under **Build and deployment**, set **Source = GitHub Actions**.
4. Go to the **Actions** tab and verify the workflow **"Publish Quarto site to GitHub Pages"** runs successfully.
5. Open your site URL again after deployment finishes.

This repo includes `.github/workflows/quarto-publish.yml` to render Quarto and deploy the built site automatically.
