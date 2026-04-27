# 🛡️ Settings Checklist — Fluxo Digital Tech

Guia único para padronizar Settings em todos os repos da organização. Aplique uma vez por repo. Itens marcados com 🔒 exigem ação manual no GitHub (não podem ser feitos via arquivos).

---

## ✅ O que já está padronizado (via arquivos no repo)

Todos os repos da fluxodigitaltech já têm:

| Item | Status |
|---|---|
| LICENSE (MIT) | ✅ |
| README profissional com badge de licença | ✅ |
| Descrição preenchida | ✅ |
| Topics relevantes | ✅ |
| Workflow gitleaks (Secret Scan semanal e por PR) | ✅ |

Repos de **código** (`project-template`, `n8n`) também têm:

| Item | Status |
|---|---|
| .gitignore | ✅ |
| .editorconfig | ✅ (project-template) |
| CONTRIBUTING.md | ✅ (project-template) |
| CODE_OF_CONDUCT.md | ✅ (project-template) |
| SECURITY.md | ✅ (project-template) |
| CHANGELOG.md | ✅ (project-template) |
| .env.example | ✅ (project-template) |
| Dependabot config | ✅ (project-template) |
| CI workflow (lint + JSON validation) | ✅ (project-template) |
| PR & Issue templates | ✅ (project-template) |
| BRANCH_PROTECTION.md (guia) | ✅ (project-template) |

---

## 🔒 Settings manuais — aplicar em cada repo

Para cada repo (`project-template`, `n8n`, `izi`, `redfitness`, `malibu`, `xnet-img`, `img-darks`, `img-darks2`, `img-izi`):

### 1️⃣ Settings → General

URL: `https://github.com/fluxodigitaltech/<REPO>/settings`

**Pull Requests:**
- ✅ Marcar **Allow squash merging**
- ❌ Desmarcar **Allow merge commits**
- ❌ Desmarcar **Allow rebase merging** (opcional, manter se preferir)
- ✅ Marcar **Always suggest updating pull request branches**
- ✅ Marcar **Allow auto-merge**
- ✅ Marcar **Automatically delete head branches**

**Features (recomendado):**
- ✅ Issues
- ✅ Discussions (opcional, para repos públicos)
- ❌ Wikis (use README/docs em vez disso)

### 2️⃣ Settings → Branches → Branch protection rules

URL: `https://github.com/fluxodigitaltech/<REPO>/settings/branches`

Clicar em **Add branch ruleset** ou **Add classic branch protection rule**, branch name pattern: `main`

- ✅ Require a pull request before merging
  - ✅ Require approvals: **1**
  - ✅ Dismiss stale pull request approvals when new commits are pushed
  - ✅ Require conversation resolution before merging
- ✅ Require status checks to pass before merging
  - ✅ Require branches to be up to date
  - Adicionar: `gitleaks` (e `lint`, `validate-json` para repos de código)
- ✅ Require linear history
- ✅ Do not allow bypassing the above settings
- ❌ Allow force pushes (DESATIVADO)
- ❌ Allow deletions (DESATIVADO)

📖 Detalhes: [`fluxodigitaltech/project-template/blob/main/.github/BRANCH_PROTECTION.md`](https://github.com/fluxodigitaltech/project-template/blob/main/.github/BRANCH_PROTECTION.md)

### 3️⃣ Settings → Code security and analysis

URL: `https://github.com/fluxodigitaltech/<REPO>/settings/security_analysis`

- ✅ Dependency graph
- ✅ Dependabot alerts
- ✅ Dependabot security updates
- ✅ Secret scanning (GitHub built-in)
- ✅ Push protection (bloqueia push com segredos)
- ✅ Private vulnerability reporting

### 4️⃣ Settings → Actions → General

URL: `https://github.com/fluxodigitaltech/<REPO>/settings/actions`

- ✅ Allow all actions and reusable workflows (ou Allow select actions, conforme política)
- ✅ Workflow permissions: **Read and write permissions** (necessário pro gitleaks comentar em PRs)
- ✅ Allow GitHub Actions to create and approve pull requests (necessário pro Dependabot)

---

## 🚨 Pendências críticas de segurança

Estes itens **devem ser feitos AGORA** — independente do checklist acima:

### 🔴 Repo `n8n`

1. **Privar o repo**: Settings → General → Danger Zone → **Change repository visibility** → Make private.
2. **Revogar a Evolution API key** `BE24D1863BF4-4594-A486-5929559842F8` exposta em `whatsapp/boas-vindas-malibu.json` no painel da Evolution API.
3. **Gerar nova credencial** e guardar apenas em `.env` local.
4. **(Opcional)** Limpar histórico do Git com [`git filter-repo`](https://github.com/newren/git-filter-repo) ou [BFG Repo-Cleaner](https://rtyley.github.io/bfg-repo-cleaner/) e force push.
5. **(Recomendado)** Re-exportar workflows do n8n com a opção **Remove credentials** ativada antes de versionar de novo.

---

## 📋 Ordem sugerida de aplicação

Para minimizar impacto:

1. **Resolver pendências críticas do n8n** (item acima).
2. Aplicar Settings em `project-template` (template oficial — vira referência).
3. Aplicar em `n8n` (já privado).
4. Aplicar nos repos de assets (`izi`, `redfitness`, `malibu`, `xnet-img`, `img-darks`, `img-darks2`, `img-izi`).

---

## ✨ Após aplicar tudo

A organização `fluxodigitaltech` terá:

- 🛡️ Branches `main` protegidas em todos os repos.
- 🔍 Secret scanning duplo (gitleaks + GitHub built-in).
- 🤖 Dependabot atualizando dependências automaticamente (no template).
- 📝 Conventional Commits enforced via PR title check.
- 🚀 Workflow padronizado: PR → CI → review → squash merge.
- 🧹 Branches deletadas automaticamente após merge.

---

> 📌 Mantenha este arquivo atualizado conforme novas regras forem adotadas.
> Versão: 1.0.0 — abril/2026
