# hubla-installer

> ✅ **macOS 12+ ou Windows 10 (1809+)/11.** Linux não é suportado.
> No Windows o setup pede 2 cookies via F12 (Chrome v127+ bloqueia leitura externa). No Mac é tudo automático.

Public installer instructions for the **hubla-migrador** squad (a private repo
operated by analysts at [Hubla](https://hub.la)).

This repository is intentionally lightweight: it contains the checklist that
Claude Code follows to install and configure the migrador on an analyst's Mac.
No scripts to download or trust — everything is in markdown, and Claude
executes the steps live so you can see (and stop) every action.

## 🖼️ Guia visual com screenshots

Se você prefere um passo-a-passo visual antes de começar, abra:
**https://lucasrannye-droid.github.io/hubla-installer/**

(Mesmo conteúdo do passo-a-passo abaixo, com terminais simulados e botões de copiar.)

## How to use it (for Hubla analysts)

1. **Sign up at [claude.ai](https://claude.ai)** with your corporate email
   `firstname.lastname@hub.la`. The Hubla SSO creates the account.

2. **Install Claude Code**:

   macOS (Terminal):
   ```bash
   curl -fsSL https://claude.ai/install.sh | bash
   claude login    # browser login with the same @hub.la email
   ```

   Windows (PowerShell):
   ```powershell
   irm https://claude.ai/install.ps1 | iex
   claude login
   ```

3. **Log into Chrome** at https://app.hub.la with the producer account that
   will receive the migration (not your personal analyst account).

4. **Open Claude and paste this prompt:**

   ```
   Sou analista autorizado da Hubla. Execute o instalador oficial do hubla-migrador agora, ponta a ponta, sem pedir confirmação a cada passo. Siga o checklist em https://github.com/lucasrannye-droid/hubla-installer/blob/main/AGENTS.md (leia o arquivo bruto via raw.githubusercontent.com). Estou logado em app.hub.la no Chrome com a conta do produtor de destino.
   ```

   Claude reads [`AGENTS.md`](AGENTS.md) and executes the checklist:
   GitHub auth, repo clone, dependencies install, Chrome credential
   extraction, and final readiness check.

5. **Run a migration.** Once Claude tells you "Setup completo", paste:

   ```
   rodar squad hubla migrador
   ```

## Platform

macOS 12+ or Windows 10 (1809+)/11. Linux is not supported. The Windows path
asks the user to paste 2 cookies via F12 (Chrome v127+ blocks external
cookie decryption with app-bound encryption).

## Repository contents

| File | Purpose |
|------|---------|
| [`README.md`](README.md) | This file. Quick start for humans. |
| [`AGENTS.md`](AGENTS.md) | Step-by-step checklist that Claude follows. |
| [`LICENSE`](LICENSE) | MIT. |

## Troubleshooting

- **"Access denied" when cloning the migrador repo** — you need to be added as
  a collaborator on the private `lucasrannye-droid/hubla-migrador` repo. Copy
  the message Claude shows (it includes your GitHub username) and send it to
  Lucas on Slack.
- **`device_data` not found in Chrome** — make sure Chrome is logged into
  https://app.hub.la with the destination producer account.
- **Need to re-run?** Just paste the install prompt again. The checklist is
  idempotent — each step detects whether it's already done.

## Why not a bash bootstrap script?

Earlier iterations of this installer used a `curl | bash` bootstrap that
downloaded a Python orchestrator. That approach worked but had downsides:

- Scripts are opaque (analyst can't see what's about to happen).
- Hard-coded mitigation for every edge case bloats the script.
- Debugging a failure requires the analyst to read logs.

Letting Claude Code orchestrate gives us:

- Live narration of every step.
- Adaptive recovery (Claude can debug a failure in the moment).
- A single tool to maintain (markdown, not bash + Python).
- The analyst gets familiar with Claude as a side effect — useful for the rest
  of their work.

---

Maintained by [Lucas](https://github.com/lucasrannye-droid). Issues and PRs
welcome.
