# Dynamic Animated GitHub Profile README Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Build the dynamic/animated profile README (plus contribution-snake workflow) specified in `docs/superpowers/specs/2026-07-27-profile-readme-design.md`, publish it, and rename the repo so it appears on github.com/pateldhruvkumar.

**Architecture:** A single `README.md` composed of third-party dynamic image services (capsule-render banner, readme-typing-svg, shields.io badges, skillicons.dev, github-readme-stats, streak-stats) — pure markdown, zero build step. One GitHub Actions workflow (`Platane/snk`) regenerates the contribution-snake SVGs daily onto an `output` branch.

**Tech Stack:** GitHub-flavored Markdown, GitHub Actions, `Platane/snk@v3`, `crazy-max/ghaction-github-pages@v4`.

## Global Constraints

- Theme: Tokyo Night — background `#1a1b27`, blue `#7aa2f7`, purple `#bb9af7`, foreground `#c0caf5`. Every stats card uses `theme=tokyonight&hide_border=true`.
- GitHub username: `pateldhruvkumar`. Final repo name: `pateldhruvkumar` (renamed from `about-me` in the last task).
- Contact links (from job-hunting master-personal-info.md): portfolio `https://dhruvvkumarpatel.vercel.app/`, LinkedIn `https://www.linkedin.com/in/dhruvkumarpatell/`, email `dhruvv.patel@outlook.com`.
- The Warehouse Logistics Associate role is intentionally omitted everywhere.
- URL checks: run from repo root with Git Bash (`curl` loop shown in each task). Every URL must return HTTP 200 except the two snake SVGs, which 404 until the final task completes.
- Windows note: run the `curl` verification loops via the Bash tool (not PowerShell).

---

### Task 1: README — header + About Me

**Files:**
- Create: `README.md`

**Interfaces:**
- Produces: `README.md` ending after the About Me section; Tasks 2–3 append below it.

- [ ] **Step 1: Create `README.md` with header and About Me**

````markdown
<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:1a1b27,50:7aa2f7,100:bb9af7&height=210&section=header&text=Dhruvkumar%20Patel&fontSize=60&fontColor=ffffff&animation=fadeIn&fontAlignY=32&desc=Software%20Developer%20%C2%B7%20AI%2FML%20%C2%B7%20Data&descAlignY=52&descSize=18" width="100%" alt="banner" />

<img src="https://readme-typing-svg.demolab.com?font=Fira+Code&weight=600&size=25&pause=1000&color=7AA2F7&center=true&vCenter=true&width=600&height=60&lines=Software+Developer;AI%2FML+Engineer;Data+Analyst;Full-Stack+Developer" alt="typing animation" />

<br/>

<a href="https://dhruvvkumarpatel.vercel.app/"><img src="https://img.shields.io/badge/Portfolio-bb9af7?style=for-the-badge&logo=vercel&logoColor=1a1b27" alt="Portfolio" /></a>
<a href="https://www.linkedin.com/in/dhruvkumarpatell/"><img src="https://img.shields.io/badge/LinkedIn-7aa2f7?style=for-the-badge&logo=linkedin&logoColor=1a1b27" alt="LinkedIn" /></a>
<a href="mailto:dhruvv.patel@outlook.com"><img src="https://img.shields.io/badge/Email-c0caf5?style=for-the-badge&logo=gmail&logoColor=1a1b27" alt="Email" /></a>
<img src="https://img.shields.io/badge/Vancouver%2C%20BC-1a1b27?style=for-the-badge&logo=googlemaps&logoColor=7aa2f7" alt="Vancouver, BC" />

<img src="https://komarev.com/ghpvc/?username=pateldhruvkumar&color=7aa2f7&style=for-the-badge&label=PROFILE+VIEWS" alt="profile views" />

</div>

## 🙋‍♂️ About Me

- 🎓 **MPS in Data Analytics (AI/ML concentration)** — Northeastern University, Vancouver · Class of 2026
- 💼 Previously **Software Developer @ Vault AI** — built an AI-powered client-intake portal for private credit firms, secure RAG pipelines over 100+ confidential documents, and QLoRA-fine-tuned Llama models
- 📊 Also **Operations Data Assistant @ Northeastern University** — MySQL + Power BI reporting and data integrity for campus operations
- 🌊 Currently building the **[Seaweed Market Intelligence Dashboard](https://seaweed-industry.vercel.app)** — a live 13-tab analytics platform with a Text-to-SQL AI assistant
- 🔍 **Open to Software / Data / AI roles** — Vancouver, BC 🇨🇦
- 📫 Reach me at **[dhruvv.patel@outlook.com](mailto:dhruvv.patel@outlook.com)**
````

- [ ] **Step 2: Verify every image URL returns 200**

Run (Bash tool):

```bash
cd /d/github/about-me && grep -o 'src="[^"]*"' README.md | sed 's/src="//;s/"$//' | while read -r u; do printf '%s %s\n' "$(curl -s -o /dev/null -w '%{http_code}' -L "$u")" "$u"; done
```

Expected: every line starts with `200`.

- [ ] **Step 3: Commit**

```bash
git add README.md
git commit -m "feat: add README header and About Me section"
```

---

### Task 2: README — Tech Stack + GitHub Stats

**Files:**
- Modify: `README.md` (append to end)

**Interfaces:**
- Consumes: `README.md` from Task 1.
- Produces: `README.md` ending after the GitHub Stats section; Task 3 appends below it.

- [ ] **Step 1: Append the Tech Stack and GitHub Stats sections**

````markdown

## 🛠️ Tech Stack

<div align="center">

**Languages**

<img src="https://skillicons.dev/icons?i=python,ts,js,r,cpp" alt="Python, TypeScript, JavaScript, R, C++" />
<br/><img src="https://img.shields.io/badge/SQL-1a1b27?style=for-the-badge&logoColor=7aa2f7" alt="SQL" />

**Frontend**

<img src="https://skillicons.dev/icons?i=react,nextjs,tailwind,vite" alt="React, Next.js, Tailwind, Vite" />

**Backend & Databases**

<img src="https://skillicons.dev/icons?i=nodejs,fastapi,supabase,postgres,mysql" alt="Node.js, FastAPI, Supabase, PostgreSQL, MySQL" />

**AI/ML & Data**

<img src="https://skillicons.dev/icons?i=pytorch,sklearn" alt="PyTorch, scikit-learn" />
<br/><img src="https://img.shields.io/badge/pandas-1a1b27?style=for-the-badge&logo=pandas&logoColor=7aa2f7" alt="pandas" /> <img src="https://img.shields.io/badge/DuckDB-1a1b27?style=for-the-badge&logo=duckdb&logoColor=7aa2f7" alt="DuckDB" /> <img src="https://img.shields.io/badge/Power%20BI-1a1b27?style=for-the-badge&logoColor=7aa2f7" alt="Power BI" /> <img src="https://img.shields.io/badge/Streamlit-1a1b27?style=for-the-badge&logo=streamlit&logoColor=7aa2f7" alt="Streamlit" /> <img src="https://img.shields.io/badge/n8n-1a1b27?style=for-the-badge&logo=n8n&logoColor=7aa2f7" alt="n8n" />

**Cloud & Tools**

<img src="https://skillicons.dev/icons?i=aws,gcp,docker,git,vercel" alt="AWS, GCP, Docker, Git, Vercel" />

</div>

## 📊 GitHub Stats

<div align="center">

<img src="https://github-readme-stats.vercel.app/api?username=pateldhruvkumar&show_icons=true&theme=tokyonight&hide_border=true&count_private=true" height="170" alt="GitHub stats" />
<img src="https://streak-stats.demolab.com?user=pateldhruvkumar&theme=tokyonight&hide_border=true" height="170" alt="GitHub streak" />

<br/><br/>

<img src="https://github-readme-stats.vercel.app/api/top-langs/?username=pateldhruvkumar&layout=compact&theme=tokyonight&hide_border=true&langs_count=8" alt="Top languages" />

</div>
````

- [ ] **Step 2: Verify every image URL returns 200**

Run (Bash tool):

```bash
cd /d/github/about-me && grep -o 'src="[^"]*"' README.md | sed 's/src="//;s/"$//' | while read -r u; do printf '%s %s\n' "$(curl -s -o /dev/null -w '%{http_code}' -L "$u")" "$u"; done
```

Expected: every line starts with `200`.

- [ ] **Step 3: Commit**

```bash
git add README.md
git commit -m "feat: add Tech Stack and GitHub Stats sections"
```

---

### Task 3: README — Latest Projects + snake + footer

**Files:**
- Modify: `README.md` (append to end)

**Interfaces:**
- Consumes: `README.md` from Task 2.
- Produces: complete `README.md`. The snake `<picture>` URLs point at the `output` branch of `pateldhruvkumar/pateldhruvkumar`, produced by Tasks 4–5.

- [ ] **Step 1: Append Projects, Contribution Graph, and footer**

````markdown

## 🚀 Latest Projects

| Project | What it is | Built with |
|---|---|---|
| 🌊 **[seaweed-industry](https://github.com/pateldhruvkumar/seaweed-industry)** · [live ↗](https://seaweed-industry.vercel.app) | 13-tab market-intelligence dashboard over 33K+ FAO/StatCan records, with a Text-to-SQL AI assistant | ![React](https://img.shields.io/badge/React-1a1b27?logo=react&logoColor=7aa2f7) ![FastAPI](https://img.shields.io/badge/FastAPI-1a1b27?logo=fastapi&logoColor=7aa2f7) ![DuckDB](https://img.shields.io/badge/DuckDB-1a1b27?logo=duckdb&logoColor=7aa2f7) |
| 🏥 **[ehealth](https://github.com/pateldhruvkumar/ehealth)** | Secure Electronic Health Records platform — Postgres Row Level Security as the security boundary, QR-code record sharing | ![Next.js](https://img.shields.io/badge/Next.js-1a1b27?logo=nextdotjs&logoColor=7aa2f7) ![Supabase](https://img.shields.io/badge/Supabase-1a1b27?logo=supabase&logoColor=7aa2f7) ![PostgreSQL](https://img.shields.io/badge/PostgreSQL-1a1b27?logo=postgresql&logoColor=7aa2f7) |
| 📦 **[end-to-end-e-commerce](https://github.com/pateldhruvkumar/end-to-end-e-commerce)** | 100K-record Olist logistics pipeline → Supabase Postgres → Excel What-If model → Power BI star schema | ![Python](https://img.shields.io/badge/Python-1a1b27?logo=python&logoColor=7aa2f7) ![PostgreSQL](https://img.shields.io/badge/PostgreSQL-1a1b27?logo=postgresql&logoColor=7aa2f7) ![Power BI](https://img.shields.io/badge/Power%20BI-1a1b27?logoColor=7aa2f7) |
| 🎭 **[transformer-microservice-gcp](https://github.com/pateldhruvkumar/transformer-microservice-gcp)** | From-scratch PyTorch transformer (4.86M params) served as a REST microservice on Cloud Run | ![PyTorch](https://img.shields.io/badge/PyTorch-1a1b27?logo=pytorch&logoColor=7aa2f7) ![Docker](https://img.shields.io/badge/Docker-1a1b27?logo=docker&logoColor=7aa2f7) ![Google Cloud](https://img.shields.io/badge/Google%20Cloud-1a1b27?logo=googlecloud&logoColor=7aa2f7) |
| ⚡ **[bigdata-final-project](https://github.com/pateldhruvkumar/bigdata-final-project)** | Event-driven serverless ETL — S3 upload → Lambda → Glue/Spark → DynamoDB, 5.6M records in one run | ![AWS](https://img.shields.io/badge/AWS-1a1b27?logo=amazonwebservices&logoColor=7aa2f7) ![AWS Lambda](https://img.shields.io/badge/Lambda-1a1b27?logo=awslambda&logoColor=7aa2f7) ![Apache Spark](https://img.shields.io/badge/Spark-1a1b27?logo=apachespark&logoColor=7aa2f7) |
| 🤖 **[agentic-kahoot-2.0](https://github.com/pateldhruvkumar/agentic-kahoot-2.0)** | Agentic quiz bot joining live games — 🥈 2nd of 15+ teams at Northeastern's Agentic AI 2.0 Hackathon | ![JavaScript](https://img.shields.io/badge/JavaScript-1a1b27?logo=javascript&logoColor=7aa2f7) ![Puppeteer](https://img.shields.io/badge/Puppeteer-1a1b27?logo=puppeteer&logoColor=7aa2f7) ![n8n](https://img.shields.io/badge/n8n-1a1b27?logo=n8n&logoColor=7aa2f7) |

## 🐍 Contribution Graph

<div align="center">

<picture>
  <source media="(prefers-color-scheme: dark)" srcset="https://raw.githubusercontent.com/pateldhruvkumar/pateldhruvkumar/output/github-snake-dark.svg" />
  <source media="(prefers-color-scheme: light)" srcset="https://raw.githubusercontent.com/pateldhruvkumar/pateldhruvkumar/output/github-snake.svg" />
  <img src="https://raw.githubusercontent.com/pateldhruvkumar/pateldhruvkumar/output/github-snake-dark.svg" alt="contribution snake" />
</picture>

</div>

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:bb9af7,50:7aa2f7,100:1a1b27&height=120&section=footer" width="100%" alt="footer" />
````

- [ ] **Step 2: Verify image URLs (snake 404s are expected here)**

Run (Bash tool):

```bash
cd /d/github/about-me && grep -oE '(src|srcset)="[^"]*"' README.md | sed -E 's/^[a-z]+="//;s/"$//' | while read -r u; do printf '%s %s\n' "$(curl -s -o /dev/null -w '%{http_code}' -L "$u")" "$u"; done
```

Expected: every line starts with `200`, **except** the three `raw.githubusercontent.com/.../github-snake*.svg` URLs which return `404` (repo not yet renamed, workflow not yet run). Also check the markdown-image badge URLs in the projects table:

```bash
cd /d/github/about-me && grep -oE '\!\[[^]]*\]\(https[^)]*\)' README.md | sed -E 's/^\!\[[^]]*\]\(//;s/\)$//' | while read -r u; do printf '%s %s\n' "$(curl -s -o /dev/null -w '%{http_code}' -L "$u")" "$u"; done
```

Expected: every line starts with `200`.

- [ ] **Step 3: Commit**

```bash
git add README.md
git commit -m "feat: add Latest Projects, contribution snake, and footer"
```

---

### Task 4: Contribution-snake workflow

**Files:**
- Create: `.github/workflows/snake.yml`

**Interfaces:**
- Produces: workflow named `Generate contribution snake` writing `github-snake.svg` and `github-snake-dark.svg` to the `output` branch — exactly the paths Task 3's `<picture>` block references.

- [ ] **Step 1: Create `.github/workflows/snake.yml`**

```yaml
name: Generate contribution snake

on:
  schedule:
    - cron: "0 6 * * *"
  workflow_dispatch:
  push:
    branches:
      - main

permissions:
  contents: write

jobs:
  generate:
    runs-on: ubuntu-latest
    timeout-minutes: 10
    steps:
      - name: Generate snake SVGs
        uses: Platane/snk@v3
        with:
          github_user_name: ${{ github.repository_owner }}
          outputs: |
            dist/github-snake.svg
            dist/github-snake-dark.svg?palette=github-dark
      - name: Push SVGs to output branch
        uses: crazy-max/ghaction-github-pages@v4
        with:
          target_branch: output
          build_dir: dist
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

- [ ] **Step 2: Validate the YAML parses**

Run (Bash tool):

```bash
cd /d/github/about-me && python -c "import yaml; yaml.safe_load(open('.github/workflows/snake.yml')); print('YAML OK')"
```

Expected: `YAML OK`. (If `yaml` is unavailable, `python -m pip install pyyaml` first.)

- [ ] **Step 3: Commit**

```bash
git add .github/workflows/snake.yml
git commit -m "ci: add contribution snake workflow"
```

---

### Task 5: Publish — push, rename repo, run workflow, verify

**Files:**
- None created; operates on the GitHub remote.

**Interfaces:**
- Consumes: all commits from Tasks 1–4; workflow `snake.yml` from Task 4.

- [ ] **Step 1: Push main**

```bash
git push -u origin main
```

- [ ] **Step 2: Rename the repo to match the username**

```bash
gh repo rename pateldhruvkumar --repo pateldhruvkumar/about-me --yes
```

Note: `gh repo rename` updates the local `origin` remote automatically when run inside the repo. Verify with `git remote -v` — expected URL `https://github.com/pateldhruvkumar/pateldhruvkumar.git`.

- [ ] **Step 3: Confirm the snake workflow ran (it triggers on push; otherwise dispatch it)**

```bash
gh run list --workflow snake.yml --repo pateldhruvkumar/pateldhruvkumar --limit 3
```

If no run is listed: `gh workflow run snake.yml --repo pateldhruvkumar/pateldhruvkumar` then re-check. Wait for status `completed`/`success` (`gh run watch <id>` or re-run the list command).

- [ ] **Step 4: Verify the snake SVGs exist on the output branch**

```bash
curl -s -o /dev/null -w '%{http_code}\n' -L https://raw.githubusercontent.com/pateldhruvkumar/pateldhruvkumar/output/github-snake-dark.svg
```

Expected: `200`.

- [ ] **Step 5: Visual verification**

Open `https://github.com/pateldhruvkumar` in the browser. Confirm: banner + typing animation render, badge row correct (LinkedIn badge may show no icon — acceptable), skill icons load, both stats cards + top-langs render in Tokyo Night, projects table shows 6 rows with badges, snake animates, footer wave renders. Report any broken image for fix-up.

- [ ] **Step 6: Final commit if fixes were needed; otherwise done**

```bash
git status
```

Expected: clean tree.
