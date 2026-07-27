# GitHub Profile README — Design Spec

**Date:** 2026-07-27
**Repo:** `pateldhruvkumar/about-me` (to be renamed `pateldhruvkumar/pateldhruvkumar` at the end so GitHub displays it on the profile page)
**Deliverables:** `README.md`, `.github/workflows/snake.yml`

## Goal

A dynamic, animated GitHub profile README for Dhruvkumar Patel that presents name, roles, about-me, skills, and latest projects in a recruiter-friendly way. Style chosen by user: **Dynamic & animated** (wave banner, typing animation, stats cards, contribution snake).

## Content sources (canonical)

All personal content comes from `D:\github\job-hunting\database\`:
`master-personal-info.md` (contact links), `master-experience.md` (roles), `master-education.md` (degrees), `master-project.md` (projects).

Role framing chosen by user: **AI-focused dev, open to work.** Headline as Software Developer & Data Analytics (AI/ML) grad — Northeastern University '26, open to Software / Data / AI roles. Past roles shown: Software Developer @ Vault AI, Operations Data Assistant @ Northeastern. The Warehouse Logistics Associate role at Save-On-Foods is intentionally omitted.

## Visual theme

Tokyo Night palette throughout: background `#1a1b27`, blue `#7aa2f7`, purple `#bb9af7`. All stats cards use `theme=tokyonight&hide_border=true`. Banner and footer gradients use the same colors.

## README structure (top to bottom)

1. **Header banner** — `capsule-render.vercel.app` waving type, gradient `0:1a1b27 → 50:7aa2f7 → 100:bb9af7`, text "Dhruvkumar Patel", height ~200.
2. **Typing animation** — `readme-typing-svg.demolab.com`, Fira Code, color `7AA2F7`, centered, cycling: `Software Developer` → `AI/ML Engineer` → `Data Analyst` → `Full-Stack Developer`.
3. **Badge row** (centered) — shields.io badges linking: Portfolio (`dhruvvkumarpatel.vercel.app`), LinkedIn (`linkedin.com/in/dhruvkumarpatell`), Email (`dhruvv.patel@outlook.com`), plus a static 📍 Vancouver, BC badge and a `komarev.com/ghpvc` profile-views counter.
4. **About Me** — emoji bullets: 🎓 MPS Data Analytics (AI/ML), Northeastern University '26; 💼 previously Software Developer @ Vault AI (AI client-intake portal, RAG pipelines over 100+ confidential docs, QLoRA fine-tuning) and Operations Data Assistant @ Northeastern; 🌊 currently building the Seaweed Market Intelligence Dashboard; 🔍 open to Software / Data / AI roles; 📫 how to reach me.
5. **Tech Stack** — `skillicons.dev` icon rows grouped with bold labels:
   - Languages: `python,ts,js,r,cpp` + SQL (shields badge)
   - Frontend: `react,nextjs,tailwind,vite`
   - Backend & Databases: `nodejs,fastapi,supabase,postgres,mysql`
   - AI/ML & Data: `pytorch,sklearn` + shields badges for pandas, DuckDB, Power BI, Streamlit, n8n
   - Cloud & Tools: `aws,gcp,docker,git,vercel`
6. **GitHub Stats** — `github-readme-stats` stats card and `streak-stats.demolab.com` side by side; compact top-languages card below; all tokyonight.
7. **Latest Projects** — table with six rows, each: emoji + repo link, one-line hook, small shields.io tech badges, live-demo link where one exists:
   - 🌊 [seaweed-industry] — 13-tab market-intelligence dashboard + Text-to-SQL AI assistant over FAO/StatCan data (live: seaweed-industry.vercel.app)
   - 🏥 [ehealth] — secure EHR platform; Postgres RLS as the security boundary, QR-code record sharing
   - 📦 [end-to-end-e-commerce] — 100K-record Olist logistics pipeline → Supabase Postgres → Power BI star schema
   - 🎭 [transformer-microservice-gcp] — from-scratch PyTorch transformer (4.86M params) served on Cloud Run
   - ⚡ [bigdata-final-project] — event-driven AWS ETL (S3→Lambda→Glue→DynamoDB), 5.6M records
   - 🤖 [agentic-kahoot-2.0] — agentic quiz bot; 🥈 2nd of 15+ teams, Northeastern Agentic AI 2.0 Hackathon
8. **Contribution snake** — dark-mode SVG referenced from the `output` branch: `raw.githubusercontent.com/pateldhruvkumar/pateldhruvkumar/output/github-snake-dark.svg` (with `<picture>` fallback to the light variant).
9. **Footer** — matching capsule-render waving footer (flipped).

## Snake workflow

`.github/workflows/snake.yml` using `Platane/snk@v3`: triggers on `schedule` (daily cron), `workflow_dispatch`, and `push` to `main`; generates `github-snake.svg` + `github-snake-dark.svg`; pushes to `output` branch via `crazy-max/ghaction-github-pages@v4` or snk's built-in push with `GITHUB_TOKEN` (needs `permissions: contents: write`).

## Error handling / known limitations

- The snake image 404s until (a) the repo is renamed and (b) the workflow has run once. Acceptable; the `<picture>` tag simply shows a broken image until then — verify after rename.
- If a `skillicons.dev` icon id doesn't exist, substitute a shields.io badge instead.
- Third-party card services (github-readme-stats, streak-stats) can be slow/rate-limited; this is cosmetic and self-heals.

## Rollout

1. Commit README + workflow to this repo, push to `main`.
2. Rename the GitHub repo `about-me` → `pateldhruvkumar` (via `gh repo rename`), update local remote URL.
3. Trigger the snake workflow once; verify the profile page renders.

## Testing

- Render check: preview README locally/on GitHub; all sections present in order.
- Link check: every image/badge URL returns 200 (except snake pre-rename, see above); all hyperlinks point to the right repos/profiles.
- Workflow check: snake action completes green and `output` branch contains both SVGs.
