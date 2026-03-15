# 🚀 GitHub Pages Setup Guide (devops-learning-2)

## 1) Push your code

```bash
cd /path/to/devops-learning-2

git add .
git commit -m "Initial publish: Python scripting course"
git push -u origin main
```

## 2) Enable GitHub Pages

1. Open your repo on GitHub
2. **Settings** → **Pages**
3. **Source**: Deploy from a branch
4. Branch: `main`
5. Folder: `/ (root)`
6. Save

After 1–5 minutes, your site will be live at:

`https://reachharsha.github.io/devops-learning-2/`

## 3) Update and redeploy

```bash
git add .
git commit -m "Update Python lessons"
git push
```
