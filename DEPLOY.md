# Deploy to GitHub Pages

## 1. Create a repo on GitHub

1. Go to [github.com/new](https://github.com/new).
2. **Repository name:**  
   - Use **`sanjaynichani.github.io`** if you want the site at `https://sanjaynichani.github.io` (and later your custom domain).  
   - Or any name (e.g. `website`); then the site will be at `https://<username>.github.io/website/` unless you set a custom domain.
3. Choose **Public**, leave “Add a README” **unchecked** (you already have files).
4. Click **Create repository**.

## 2. Connect this folder to GitHub

In a terminal, from the **website** folder (the one that contains `sanjaynichani` and `.github`):

```bash
cd /Users/sanjay/develop/website

# Initialize git if this folder isn’t a repo yet
git init

# Stage everything
git add .

# First commit
git commit -m "Initial commit: static site for GitHub Pages"

# Add your GitHub repo as remote (replace YOUR_USERNAME and REPO with your values)
# If you used sanjaynichani.github.io:
git remote add origin https://github.com/YOUR_USERNAME/sanjaynichani.github.io.git

# If your default branch is main (GitHub’s default)
git branch -M main

# Push and set upstream
git push -u origin main
```

Use your GitHub username in place of `YOUR_USERNAME`. If you use a different repo name, change `sanjaynichani.github.io` in the URL to match.

## 3. Turn on GitHub Pages (Actions)

1. On GitHub, open your repo → **Settings** → **Pages** (left sidebar).
2. Under **Build and deployment**:
   - **Source:** choose **GitHub Actions**.

No need to pick a branch or folder; the workflow will deploy when you push.

## 4. After the first push

- The **Deploy to GitHub Pages** workflow will run on every push to `main`.
- When it finishes, the site is at:
  - `https://YOUR_USERNAME.github.io/sanjaynichani.github.io/` if the repo is `sanjaynichani.github.io`, or  
  - `https://YOUR_USERNAME.github.io/REPO_NAME/` for any other repo name.
- To use **sanjaynichani.com**: in the same **Pages** settings, set **Custom domain** to `sanjaynichani.com`, then add the DNS records GitHub shows you at your domain registrar (e.g. Hover).

## 5. Later: make changes and redeploy

```bash
git add .
git commit -m "Describe your change"
git push
```

The workflow will run again and update the live site.
