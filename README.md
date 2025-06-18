# 🚀 DevSecOps App Template

[![CI / CD](https://github.com/RStaff/app-template/actions/workflows/ci.yml/badge.svg)](https://github.com/RStaff/app-template/actions/workflows/ci.yml)

A one-click starter repo for **Python + Docker** micro-services with a *full* GitHub-Actions DevSecOps pipeline:

| Stage            | What happens automatically                                   |
|------------------|--------------------------------------------------------------|
| **Build**        | Docker image built with Buildx layer cache                   |
| **Unit test**    | `pytest` (or skipped if no tests yet)                        |
| **Static scan**  | Bandit (Python security linter)                              |
| **Dependency scan** | Trivy CVE scan on the container                           |
| **Push**         | Image tagged `ghcr.io/<owner>/<repo>:<sha>` and pushed to GHCR |
| **Deploy (optional)** | Pulls image on VPS / Render / Fly.io (edit `ci.yml`)    |
| **Alerts**       | Slack webhook on failure (add `SLACK_WEBHOOK_URL` secret)    |

Mark this repo as a **template** and every new project inherits the pipeline, Dockerfile, and folder layout—no copy-paste required.

---

## 📂 Folder structure

```text
.github/
  workflows/ci.yml      ← CI/CD pipeline
app/
  __init__.py           ← your package code
  main.py               ← simple “Hello DevSecOps”
Dockerfile              ← production container
requirements.txt        ← runtime deps (Flask 3.0.2)
README.md               ← you’re here


---

## ⚡ Quick start

### 1. Generate a new service

```bash
gh repo create my-api --template RStaff/app-template --public
git clone https://github.com/RStaff/my-api.git
cd my-api

Run locally :
python -m venv .venv && source .venv/bin/activate
pip install -r requirements.txt
python app/main.py          # prints “Hello DevSecOps”

 Push code and watch the pipeline:
git commit --allow-empty -m "chore: trigger CI"
git push -u origin main

🐳 Build the image locally
docker build -t my-api:dev .
docker run --rm my-api:dev

