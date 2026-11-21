<div align="center">

# 🪞 IR Mirrors for Agents

**Switch your development tools to fast Iranian mirrors — safely, automatically, and only where you want them.**

[![Catalog: 20+ providers](https://img.shields.io/badge/catalog-20%2B%20providers-blue)](MIRROR_CATALOG.md)
[![Tools: 20+ supported](https://img.shields.io/badge/tools-20%2B%20supported-success)](MIRROR_CATALOG.md#part-3--configuration-playbook)
[![Verified: 2026‑11‑19](https://img.shields.io/badge/verified-2026--11--19-orange)](#-how-the-data-was-built)
[![Prompt: EN + FA](https://img.shields.io/badge/prompt-EN%20%2B%20FA-informational)](AGENT_PROMPT_EN.md)
[![README: EN + FA](https://img.shields.io/badge/readme-EN%20%2B%20FA-informational)](README.fa.md)

</div>

---

<div align="center">

https://github.com/user-attachments/assets/45812c1d-833b-49fe-94f7-cf0c9e95e1d5

*▶ Watch the 60-second promo — the agent interviews, mirrors, tests, and reports, end to end.*

</div>

## ✨ What is this?

A small, self-contained toolkit that lets **any coding agent** (Claude Code, ZCode, Cursor, Copilot Workspace, …) configure Iranian package mirrors on your machine:

- 🧠 **It asks before it touches anything** — you choose the tools, nothing else is modified.
- 🧪 **It tests every change** — a mirror counts as configured only if it actually delivers a package.
- 🔁 **It falls back automatically** — if a mirror fails its test, the agent reverts and tries the next source in the chain.
- 📜 **It reports faithfully** — final summary of what changed, what passed, what failed, and how to roll back.

All mirror data was compiled from [thealibigdeli.ir/mirrors](https://thealibigdeli.ir/mirrors) and **verified provider-by-provider on 2026-11-19** (every endpoint fetched and probed).

## 📦 What's inside

| File | Purpose |
|---|---|
| 📚 [MIRROR_CATALOG.md](MIRROR_CATALOG.md) | **The single source of truth.** Detailed coverage of every provider (Part 2) + per-tool ordered mirror options with configure/test/revert commands (Part 3) |
| 🤖 [AGENT_PROMPT_EN.md](AGENT_PROMPT_EN.md) | The agent operating prompt — English |
| 🤖 [AGENT_PROMPT_FA.md](AGENT_PROMPT_FA.md) | The agent operating prompt — Persian (فارسی) |
| 📖 [README.md](README.md) | This file — English |
| 📖 [README.fa.md](README.fa.md) | Persian user guide (راهنمای فارسی) |

## 🚀 Quickstart

> Requires: any coding agent that can run shell commands, and `MIRROR_CATALOG.md` in the working directory.

1. **Open your coding agent** in this folder.
2. **Paste the prompt** — either [AGENT_PROMPT_EN.md](AGENT_PROMPT_EN.md) or [AGENT_PROMPT_FA.md](AGENT_PROMPT_FA.md), everything below the divider line.
3. **Answer the interview.** The agent shows you a numbered menu of supported tools — reply with the ones you want, e.g.:

   > `2 and 4` — *npm and Ubuntu apt only*

4. **Watch it work.** For each tool the agent will:
   back up → configure → test → on failure revert & try the next mirror → report.

Done. Nothing else on your system is touched.

## 🧠 How the agent behaves

```text
      ┌──────────────────────────────────────────────────────────┐
      │  Step 1 · INTERVIEW                                      │
      │  "Which tools should I switch to Iranian mirrors?"       │
      │  → user picks ONLY the tools they use                    │
      └──────────────────────────┬───────────────────────────────┘
                                 ▼
      ┌──────────────────────────────────────────────────────────┐
      │  Step 2 · PLAN (per tool, from the catalog)              │
      │  pip → ①RunFlare → ②Chabokan → ③IranServer → …           │
      └──────────────────────────┬───────────────────────────────┘
                                 ▼
      ┌──────────────────────────────────────────────────────────┐
      │  Step 3 · EXECUTE (one tool at a time)                   │
      │   backup → apply option ① → TEST                         │
      │                 ├─ pass ✅ → next tool                   │
      │                 └─ fail ❌ → revert → apply ② → TEST     │
      │                              └─ fail ❌ → revert → ③ …   │
      │      all options failed → leave tool untouched           │
      └──────────────────────────┬───────────────────────────────┘
                                 ▼
      ┌──────────────────────────────────────────────────────────┐
      │  Step 4 · REPORT (table + changes + rollback commands)   │
      └──────────────────────────────────────────────────────────┘
```

**Testing is honest:** a mirror that merely responds isn't a pass — the mirror must deliver the actual artifact (a downloaded package, a successful `apt-get update`, a pulled image). Failures are classified as transient (one retry at 2× timeout) or deterministic (immediate fallback).

## ✅ Supported tools (20+)

| | Tool | | Tool | | Tool |
|---|---|---|---|---|---|
| 🐍 | pip / PyPI | 🟢 | Node.js / npm (+ yarn, pnpm) | 🐹 | Go modules |
| 🐳 | Docker Hub images | 🐧 | Ubuntu apt | 🐧 | Debian apt |
| 🏛️ | Docker CE & third-party apt repos | 🏛️ | Arch / Alpine / Fedora | 🏛️ | CentOS / Alma / Rocky / EPEL |
| 🏛️ | Kali / Manjaro / openSUSE / Mint / Raspbian | 🎯 | Flutter / Dart (pub.dev) | 🦀 | Rust / Cargo |
| ☕ | Maven & Gradle | 🐘 | Composer (PHP) | 🔷 | NuGet (.NET) |
| 💎 | RubyGems | 🤗 | Hugging Face | 🧩 | VS Code extensions |
| 🤖 | Android SDK | 🟩 | nvm & pyenv | 🍺 | Homebrew (macOS) |
| ☸️ | Kubernetes (pkgs.k8s.io, kubeadm, Helm) | 💿 | OS ISO downloads (Ubuntu/Debian/Windows) | | |

For every tool the catalog lists **multiple mirror options from different providers**, ordered by a fallback priority — exactly the case in the task: *"if multiple mirrors are available for a single tool (like Docker), the agent must proceed to the next option if the first one fails the test."* Docker alone has **12 options**.

## 🪞 Provider coverage (highlights)

| Provider | Strengths | Status* |
|---|---|---|
| 🏢 **RunFlare** | Broadest registry set: Docker, PyPI, npm, Go, Flutter, Maven, NuGet, K8s, Node dist + 7 Linux distros | ✅ |
| 🏢 **IranServer** | Everything + RubyGems, Cargo, K8s (`pkgs.k8s.io` layout), huge ISO library (incl. Windows, ESXi, Proxmox) | ✅ |
| 🏢 **DevNeeds** | The long tail: Flutter/pub.dev, Hugging Face, VS Code extensions, Android SDK, Homebrew, Windows Update, third-party apt repos | ✅ (geo-WAF abroad) |
| 🏢 **ArvanCloud** | Ubuntu/Debian apt + Docker registry cache — the source page's own recommendation | ✅ |
| 🏢 **Liara** | Pull-through caches for Docker, PyPI, npm, Go, Composer, apt | ✅ |
| 🏛️ **Jamko / chrepo** | Government-backed registry set incl. Helm, Gradle, Android, RPM repo files | ✅ |
| 🏢 **MobinHost / Sindad / Pishgaman / Shatel / Rasanegar / AminiDC / IUT** | Classic Linux distro archives + ISOs, many same-day fresh | ✅ |
| 🏛️ **ITO national repo** | ~70 repos, security-reviewed, incl. AI/LLM caches | ✅ |
| 🏢 **Megan / Pardisco / Asiatech** | Broad registries / Ubuntu+Docker caches | ⚠️ flagged at probe |
| ❌ **KubarCloud / HyperClouds / Rust-Meetup** | Listed on the source page, **dead at verification** (documented so the agent skips them) | ❌ |

\* full per-endpoint detail in [Part 2 of the catalog](MIRROR_CATALOG.md#part-2--provider-directory).

## 🛠️ Manual use (no agent)

Everything is ordinary shell:

1. Open [MIRROR_CATALOG.md](MIRROR_CATALOG.md) → **Part 3** → your tool.
2. Take **option 1** from the table, run the *configure* snippet with that endpoint.
3. Run the *test* command. If it fails, take option 2, **first** reverting per the *revert* line.

## 🔐 Safety & caveats

- 🗂️ **Backups:** every modified file gets a `.bak-YYYYMMDD-HHMMSS` sibling; the final report includes a rollback block.
- 🛑 **No silent downgrades:** options needing `trusted=yes`, `strict-ssl false`, or `GOSUMDB=off` are applied only with your explicit approval (the agent must tell you first).
- 🌍 **Vantage point matters:** the verification was run from outside Iran. Services that geo-block foreign IPs (DevNeeds ⚠️) may work *better* for you; conversely always re-test on your own machine — the agent does this automatically.
- ⚖️ **Quotas & quirks:** RunFlare free tier = 2,000 requests/IP; Chabokan's apt repos are unsigned; a few mirrors serve plain HTTP. All flagged in the catalog.
- 🩹 **Worst case:** if every option for a tool fails, the agent leaves that tool untouched — you only lose time, not configuration.

## 🔄 How the data was built

1. The provider list was scraped from [thealibigdeli.ir/mirrors](https://thealibigdeli.ir/mirrors) (plus the site's `/pypi-alternative` and `/ubuntu-solutions` pages and their scripts).
2. **Every provider page** was fetched and every endpoint probed (registry `/v2/`, PyPI `/simple/`, npm packuments, apt `/dists/`, directory listings).
3. Coverage, freshness, and quirks were recorded per provider → [MIRROR_CATALOG.md](MIRROR_CATALOG.md).
4. Catalog is dated **2026-11-19** — mirrors come and go; re-run a verification before relying on a rarely-used option, and see the FAQ below.

## ❓ FAQ

<details>
<summary><b>Will the agent change tools I didn't ask about?</b></summary>
No. Rule #1 of the prompt is "ask first, configure second", rule #2 is "minimum footprint". The Docker-only user gets Docker-only changes.
</details>

<details>
<summary><b>What if a mirror dies next week?</b></summary>
The agent tests before trusting: a dead mirror fails its test and the agent automatically moves to the next option in that tool's chain. To refresh the catalog itself, re-run the verification (see <a href="#-how-the-data-was-built">How the data was built</a>).
</details>

<details>
<summary><b>Windows / macOS support?</b></summary>
The catalog targets POSIX-style configs but includes Windows notes (e.g. <code>setx</code> for env vars, <code>%APPDATA%\pip\pip.ini</code>), and the prompt tells the agent to detect the OS and adapt. Docker daemon config works the same everywhere.
</details>

<details>
<summary><b>Why do some tools have only one or two options?</b></summary>
Coverage honestly reflects what exists: e.g. RubyGems is mirrored only by IranServer, and KubarCloud/HyperClouds were found dead. Undocumented guesses are deliberately absent.
</details>

<details>
<summary><b>Can I use this on a server / CI?</b></summary>
Yes — for non-interactive runs, pass the tool list to the agent up front (e.g. "configure pip, npm and docker; skip the interview") and it will skip Step 1 accordingly; backups and the report still apply.
</details>

## 🙏 Credits

- 🪞 Mirror list & ecosystem knowledge: [Ali Bigdeli — thealibigdeli.ir/mirrors](https://thealibigdeli.ir/mirrors)
- 🏛️ Mirror infrastructure: RunFlare, ArvanCloud, IranServer, Chabokan, Liara, DevNeeds, Jamko/chrepo, Megan, MobinHost, Pardisco, Asiatech, ITO, IUT IT Center, Sindad, Pishgaman, Shatel, Rasanegar, AminiDC — and the operators behind every endpoint in the catalog.

## 📬 Contact Me

- ▶️ YouTube: [@Ryan-Heida](https://www.youtube.com/@Ryan-Heida)
- ✈️ Telegram: [@RyanHeida](https://t.me/RyanHeida)
- 💼 LinkedIn: [Ryan Heida](https://www.linkedin.com/in/ryan-heida)
- 📧 Email: [mr.ryanheida@gmail.com](mailto:mr.ryanheida@gmail.com)
- 🐙 GitHub: [Ryan-PG](https://www.github.com/Ryan-PG)
- 🐦 X (Twitter): [@Ryan_Heida_](https://x.com/Ryan_Heida_)

<div align="center">

**Made for developers who just want their packages to download.** 📦⚡

</div>
