<!-- FactFuse README.md -->

<p align="center">
  <img src="https://raw.githubusercontent.com/your-org/factfuse/main/docs/assets/logo.svg" alt="FactFuse Logo" width="150"/>
  <h1 align="center">FactFuse</h1>
  <p align="center"><em>Fuse Truth with Technology</em></p>
  <p align="center">
    <a href="https://github.com/your-org/factfuse/blob/main/LICENSE"><img src="https://img.shields.io/badge/License-MIT-blue.svg" alt="License"></a>
    <a href="https://github.com/your-org/factfuse/actions/workflows/ci.yml"><img src="https://img.shields.io/github/actions/workflow/status/your-org/factfuse/ci.yml?branch=main" alt="CI Build"></a>
    <img src="https://img.shields.io/badge/Version-1.1-orange.svg" alt="Version">
  </p>
</p>

---
🆚 Version 1.1 • 📅 June 7, 2025

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

🔍 EXECUTIVE SUMMARY
FactFuse is an open-source, zero-cost AI fact-checking platform. It automatically processes social media content (Facebook, Twitter, LinkedIn, Reddit), extracts factual claims, retrieves evidence using hybrid search (Milvus + Elasticsearch), and generates fully cited verdicts via OpenRouter’s DeepSeek free model. No hallucinations, and low-confidence results are flagged for review.

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

🎯 OBJECTIVES
• ✅ Accuracy & Trust – Source-backed citations in every verdict
• 💸 Zero Licensing – 100% free models and open-source stack
• ⚡ Scalable – Sub-second responses with microservice architecture
• 🔧 Extensible – Modular, docs-as-code, and easy contributions
• 🔗 Multi-Platform – Works with Facebook, Twitter, LinkedIn, Reddit via API/webhooks

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

🔁 FACT-CHECKING PIPELINE

1️⃣ Ingestion
• Facebook Graph API, Twitter, LinkedIn, Reddit via webhook adapters
• Payload normalized into "claim" object via FastAPI

2️⃣ Claim Extraction
• spaCy + transformer classifier detects factual claims
• Entity & POS tagging isolates key terms

3️⃣ Evidence Retrieval
• Hybrid search: Milvus (vector) + Elasticsearch (keyword)
• Deduplicated Top-K snippets selected

4️⃣ Reranking
• MonoT5 re-scores relevance
• Filters apply recency & authority checks

5️⃣ Grounded Verdict Generation
• Prompted with numbered evidence snippets only
• DeepSeek model outputs verdicts like: “Claim is unsupported [1][3].”

6️⃣ Verification
• All citations are re-queried for support
• Unsupported outputs flagged for human moderation

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

⚙️ SYSTEM ARCHITECTURE
Services: REST/gRPC over Docker + k3s, reverse-proxied by NGINX
• 🌐 API Gateway – FastAPI + Uvicorn
• 📥 Claim Extraction – spaCy + Transformers
• 📚 Retrieval – Milvus + Elasticsearch
• 🧠 Reranker – MonoT5
• 📝 Generator – OpenRouter DeepSeek
• 🕵️ Verification – Auto re-checks
• 🖼️ Image Service – OpenCV, Tesseract, CLIP
• 🔁 Redis Cache
• 🗃️ PostgreSQL DB
• 🧺 MinIO Object Store
• 📊 Monitoring – Prometheus, Grafana, Loki

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

🧩 TECH STACK OVERVIEW

• ⚡ FastAPI, Uvicorn, NGINX
• 🧠 NLP: spaCy, Transformers
• 🔍 Search: Milvus, Weaviate, Elasticsearch
• 🧬 Embeddings: Sentence-Transformers
• 🗂️ Reranker: cross-encoder/ms-marco-MiniLM-L-6-v2
• ✍️ LLM: DeepSeek via OpenRouter (free-tier)
• 🖼️ CLIP + Tesseract for OCR
• 🧱 DB: PostgreSQL, Redis, MinIO
• 📦 Docker, k3s, Terraform
• 🛠️ CI: GitHub Actions
• 📚 Docs: MkDocs Material + Mermaid

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

🧰 FEATURES

• 🌐 Browser Extension – Inline claim validation
• 🌍 Multi-language UI + RTL support
• 📈 TrustScore – From source credibility and cross-source overlap
• 📊 Analytics Dashboard
• 🗳️ Community Feedback with moderation queue
• 🔌 Public REST API + SDKs for Python & JS

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

🛡️ NON-FUNCTIONAL GOALS
• ⏱️ ≤ 300 ms median response
• 🌐 99.9% uptime
• 🔒 TLS + API keys/OAuth2 + OWASP compliance
• 📦 Auto-scaling stateless services
• 🧪 80%+ test coverage, CI linting

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

🎨 UX DESIGN
Palette:
• 🎨 Navy: #003366, Light Blue: #336699, Green: #27AE60
• ⚠️ Alert Orange: #F2994A, Gray BG: #F5F5F5
Fonts:
• Headings: Inter Bold
• Body: Roboto / Open Sans Regular
Layout:
• 🔲 Card-based, 2-column responsive UI
Accessibility:
• 🦮 WCAG 2.1 AA + ARIA + keyboard nav

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

🚀 DEPLOYMENT PLAN (WEEKLY)

• Week 1–2: Provision free VPS or local k3s, Dockerize services
• Week 3–4: Launch Milvus/Elasticsearch; build claim extractor
• Week 5–6: Full RAG pipeline; image OCR
• Week 7–8: Browser extension + dashboards
• Week 9–10: CI/CD with GitHub Actions, Terraform infra, alerting

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

🔍 QUALITY CONTROL

• 🔁 Testing: pytest, Jest, nightly regression
• 🧪 Static checks: flake8, mypy, ESLint
• 📊 Metrics: Prometheus + Grafana
• 📄 Logs: Loki JSON
• 🚨 Alerts: 5xx errors, resource spikes, slow responses
• 🔎 Monthly audits: 100 sample verdicts

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

📚 DOCUMENTATION

• 🧭 Hosted with MkDocs + Mermaid diagrams
• 🖼️ Assets in /docs/assets/
• 📄 PDF exports with page numbers and headers
• Templates: ISSUE_TEMPLATE.md, CONTRIBUTING.md, CODE_OF_CONDUCT.md

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

🛤️ FUTURE ROADMAP

• 📊 Explainability dashboard
• 🔐 Blockchain audit trail
• 📱 Native Flutter mobile apps
• 💬 Bots for Slack, Teams, WhatsApp
• 🎥 Video deepfake detection
• 🧠 Model upgrades: Mistral, Falcon, fine-tuning
• ⚖️ Bias/sentiment detection

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

🤝 CONTRIBUTING & GOVERNANCE

• Folder structure: /api, /retriever, /ui, /docs, /infra
• 🧾 Guidelines in CONTRIBUTING.md
• ✅ Code of Conduct enforced
• 🏆 Contributor recognition, monthly sync calls, “good first issues”

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

📎 APPENDICES & REFERENCES

• DeepSeek Free Model: deepseek/deepseek-transformer-7b:free
• API Docs: https://docs.openrouter.ai
• FastAPI: https://fastapi.tiangolo.com
• Milvus: https://milvus.io
• MkDocs: https://squidfunk.github.io/mkdocs-material/
• Terraform: https://terraform.io
• Prometheus: https://prometheus.io
• Grafana: https://grafana.com

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
End of README
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

