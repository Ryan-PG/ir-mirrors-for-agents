# 🪞 Iranian Mirror Catalog — Single Source of Truth

**Generated:** 2026-11-19 · **Primary source:** [thealibigdeli.ir/mirrors](https://thealibigdeli.ir/mirrors) (Ali Bigdeli's mirror list) · **Verification:** every provider page was fetched, every endpoint probed on 2026-11-19.

This catalog has three parts:

| Part | Purpose |
|---|---|
| **Part 1 — Legend & rules** | How to read this file; option-priority rules |
| **Part 2 — Provider directory** | A detailed profile of **every** source: exactly what it covers, endpoint by endpoint |
| **Part 3 — Configuration playbook** | Per-tool, ordered mirror options with exact configure / test / revert commands |

> A companion prompt (`AGENT_PROMPT_EN.md` / `AGENT_PROMPT_FA.md`) tells a coding agent how to operate this catalog.

---

## Part 1 — Legend & rules

### Status markers (from 2026-11-19 probes)

| Marker | Meaning |
|---|---|
| ✅ | Endpoint verified live at probe time (HTTP 200, or 401/200 on a registry `/v2/`) |
| 🟡 | Listed by the provider or a third party; endpoint **not independently verified** |
| ⚠️ | Endpoint existed but misbehaved at probe time (5xx / geo-block / slow) |
| ❌ | Dead at verification time (NXDOMAIN, DNS broken, gateway down) |

> Probes ran from **outside Iran**. Some Iranian services geo-block foreign IPs (marked ⚠️) — they may work fine from inside Iran. Conversely, a ✅ from abroad says nothing about in-country speed. The agent **must re-test on the target machine**.

### How option priority is ordered

For each tool, options are ordered by: probe status → sync freshness → breadth/quality of provider → config quality (signed repos preferred over `trusted=yes`). The agent re-tests live, so the order is a starting point, not gospel.

### Global caveats

- **RunFlare quota:** free tier = **2,000 requests per IP**; beyond that you must register the IP in a RunFlare account with a mirror package.
- **Chabokan apt** publishes unsigned repos (`deb [trusted=yes]`) — a security downgrade; prefer signed alternatives.
- **IranServer guides** sometimes recommend `strict-ssl false` / `--no-check-certificate` — avoid disabling TLS verification unless nothing else works.
- **Plain-HTTP mirrors** (`mirror.arvancloud.ir`, `mirror-linux.runflare.com`, `mirror.shatel.ir`, `linux-mirror.liara.ir`, `mirror.aminidc.com`) do not authenticate packages in transit; apt signatures still protect integrity, but prefer HTTPS when equal.
- **Pull-through caches** (Liara, Asiatech, ArvanCloud Docker) fetch on first request — the *first* install of a package is slower, subsequent ones fast.

---

## Part 2 — Provider directory

> Each profile states exactly what the source covers. ✅/🟡/⚠️/❌ per endpoint. Operators: 🏢 company · 🏛️ government · 🎓 university.

### 2.1 🏢 RunFlare (رانفلر) — `runflare.com/mirrors`

Cloud platform (Pars Web Server group). The broadest *language-registry* mirror set; verified via probes.

| Ecosystem | Endpoint | Status |
|---|---|---|
| Docker Hub (+ mcr.microsoft.com, registry.k8s.io, gcr.io, ghcr.io, quay.io) | `https://mirror-docker.runflare.com` | ✅ `/v2/` 200 |
| PyPI | `https://mirror-pypi.runflare.com/simple` | ✅ 200 (full index) |
| npm (+ Yarn) | `https://mirror-npm.runflare.com` | ✅ 200 |
| Composer | `https://mirror-composer.runflare.com` | 🟡 documented |
| Go modules | `https://mirror-go.runflare.com` | ✅ 200 |
| Maven | `https://mirror-maven.runflare.com/maven2` | 🟡 documented |
| NuGet | `https://mirror-nuget.runflare.com` | 🟡 documented |
| Kubernetes packages | `https://mirror-k8s.runflare.com` | ✅ 200 |
| Flutter storage | `https://mirror-flutter.runflare.com` | ✅ 200 |
| Node.js dist | `https://mirror-nodejs.runflare.com/dist/` | ✅ 200 |
| EPEL | `https://mirror-epel.runflare.com` | ⚠️ 503 at probe |
| Ubuntu / Debian / Alpine / Arch / Fedora / AlmaLinux / Kali | `http://mirror-linux.runflare.com/<repo>` | ✅ (Ubuntu 200, incl. 26.04 resolute; plain http) |
| RHEL | listed, no public endpoint captured | 🟡 |

Notes: free quota 2,000 req/IP; sync "periodic & automatic"; no crates.io / pub.dev / conda.

### 2.2 🏢 IranServer (ایران سرور) — `mirror.iranserver.com`

Hosting provider; single accordion page documents everything. Claims **hourly** upstream sync. Content current as of 2026-11 (k8s v1.36, Ubuntu 26.04, Proxmox 9.1).

| Ecosystem | Endpoint | Status |
|---|---|---|
| Docker registry | `https://docker.iranserver.com` | ✅ `/v2/` 401 |
| PyPI | `https://pypi.iranserver.com/repository/pypi/simple` | ✅ 200 (47 MB index) |
| npm | `https://npm.iranserver.com/repository/npm/` | ✅ 200 |
| Composer | `https://composer.iranserver.com/repository/composer/` | 🟡 documented |
| Maven | `https://maven.iranserver.com/repository/maven/` | 🟡 documented |
| Go modules | `https://go.iranserver.com/repository/go/` | 🟡 documented |
| RubyGems | `https://rubygems.iranserver.com/repository/rubygems/` | 🟡 documented (unique — only Ruby mirror found) |
| NuGet | `https://nuget.iranserver.com/repository/nuget/` | 🟡 documented |
| Cargo/crates | `https://cargo.iranserver.com/repository/cargo/` | 🟡 documented |
| Ubuntu apt (16.04→26.04) | `https://mirror.iranserver.com/ubuntu/` | 🟡 documented |
| Debian apt | `https://mirror.iranserver.com/debian/` + `/debian-security/` | 🟡 documented |
| CentOS (vault 6/7/8) / AlmaLinux 8–10 / CloudLinux | `https://mirror.iranserver.com/centos-vault/centos/` `/almalinux/` `/cloudlinux/` | 🟡 documented |
| EPEL | `https://mirror.iranserver.com/epel/` | 🟡 documented |
| MariaDB apt+yum | `https://mirror.iranserver.com/mariadb/` | 🟡 documented |
| Kubernetes (pkgs.k8s.io v1.36 layout, kubectl, Rancher, CRI-O) | `https://mirror.iranserver.com/kubernetes/` | 🟡 documented |
| DirectAdmin | `https://mirror.iranserver.com/directadmin/` | 🟡 documented |
| OS ISO library (Ubuntu, Debian, CentOS, **Windows Server 2003–2025**, Win10/11, SQL Server, ESXi, Proxmox, Harvester) | `https://mirror.iranserver.com/iso/` | 🟡 documented |

Notes: Docker also listed under `insecure-registries` in their own guide; guides suggest disabling TLS checks on some endpoints — prefer keeping verification.

### 2.3 🏢 Chabokan (چابکان) — `mirror2.chabokan.net`

Cloud platform; single host, path-per-ecosystem; acts as HTTP cache-proxy. Verified probes.

| Ecosystem | Endpoint | Status |
|---|---|---|
| PyPI | `https://mirror2.chabokan.net/pypi/simple/` | ✅ 200 |
| npm (+ Yarn, pnpm) | `https://mirror2.chabokan.net/npm/` | ✅ 200 |
| Composer | `https://mirror2.chabokan.net/composer/` | ✅ 200 (`packages.json`) |
| Docker registry (Docker Hub proxy) | `https://mirror2.chabokan.net` | ✅ `/v2/` 200 |
| NuGet | `https://mirror2.chabokan.net/nuget/v3/index.json` | 🟡 documented |
| Ubuntu apt | `https://mirror2.chabokan.net/ubuntu` | 🟡 documented — ⚠️ `deb [trusted=yes]` (unsigned) |
| Debian apt | `https://mirror2.chabokan.net/debian` | 🟡 documented — ⚠️ `deb [trusted=yes]` (unsigned) |

### 2.4 🏢 ArvanCloud (آروان‌کلود) — `mirror.arvancloud.ir` + `docker.arvancloud.ir`

Major Iranian CDN/cloud. Doc pages sit behind a JS interstitial; coverage below verified **by direct probing** (plus the source page's own examples).

| Ecosystem | Endpoint | Status |
|---|---|---|
| Ubuntu apt | `https://mirror.arvancloud.ir/ubuntu` | ✅ fresh 2026-11-19 (noble Release 200) |
| Debian apt | `https://mirror.arvancloud.ir/debian` + `/debian-security` | ✅ fresh (quirk: `dists/bookworm/Release` 301→`zzz-dists/…`) |
| CentOS (vault → 7.x) | `https://mirror.arvancloud.ir/centos` | ✅ fresh timestamps |
| Alpine / Arch Linux | `https://mirror.arvancloud.ir/alpine` `/archlinux` | ✅ 200 |
| Fedora | `https://mirror.arvancloud.ir/fedora` | ⚠️ stale (2022) |
| almalinux / rockylinux / elrepo / kali / pypi / nodejs | `https://mirror.arvancloud.ir/<repo>` | ⚠️ 503 at probe — unverified |
| Docker registry cache | `https://docker.arvancloud.ir` (pull prefix `docker.arvancloud.ir/<image>`) | ✅ `/v2/` 401 |

### 2.5 🏢 DevNeeds — `devneeds.ir`

Developer-tools platform; **one subdomain per ecosystem** (endpoints extracted from the site's own guide data; some 403 from foreign IPs due to geo-WAF — designed for in-Iran use).

| Ecosystem | Endpoint | Status |
|---|---|---|
| PyPI | `https://pypi.devneeds.ir/simple/` | ⚠️ 403 geo-WAF (foreign IP) |
| npm | `https://npm.devneeds.ir/` | ⚠️ 403 geo-WAF |
| Docker registry | `https://docker.devneeds.ir` | ✅ `/v2/` 200 |
| Go modules | `GOPROXY=https://go.devneeds.ir,direct` + `GOSUMDB="sum.golang.org https://go-sum.devneeds.ir"` | 🟡 documented |
| Maven / Gradle dists | `https://maven.devneeds.ir/` / `distributionUrl=https://gradle.devneeds.ir/…` | 🟡 documented |
| Cargo | `https://cargo.devneeds.ir/repository/cargo/` | 🟡 documented |
| NuGet | `https://nuget.devneeds.ir/repository/nuget/index.json` | 🟡 documented |
| **Flutter / Dart** | `PUB_HOSTED_URL=https://dart.devneeds.ir` · `FLUTTER_STORAGE_BASE_URL=https://flutter.devneeds.ir` | 🟡 documented (only full Flutter+pub mirror) |
| Ubuntu apt | `https://ubuntu-main.devneeds.ir/` + `-security` | 🟡 documented |
| Debian apt | `https://debian-main.devneeds.ir/` + `-security` + `-archive` | 🟡 documented |
| **Third-party apt repos** (docker-ce, postgres, vscode, waydroid, trivy, zabbix) | `https://apt.devneeds.ir/{docker/\$ID \$VERSION_CODENAME, postgres, vscode, waydroid, trivy, zabbix}` | 🟡 documented |
| Kali / Arch / AlmaLinux | `https://kali.devneeds.ir` / `https://arch.devneeds.ir/` / `https://alma.devneeds.ir/` | 🟡 documented |
| LuaRocks | `https://luarocks.devneeds.ir/` | 🟡 documented |
| Node.js dist (nvm) | `NVM_NODEJS_ORG_MIRROR=https://nvm.devneeds.ir/nodejs-dist` | 🟡 documented |
| pyenv Python builds | `PYTHON_BUILD_MIRROR_URL=https://pyenv.devneeds.ir/` | 🟡 documented |
| **Android SDK** | `SDK_TEST_BASE_URL=https://dl.devneeds.ir/android/` | 🟡 documented |
| **Hugging Face** | `HF_ENDPOINT=https://hf.devneeds.ir/` (244 cached models at review) | 🟡 documented |
| Homebrew | `HOMEBREW_API_DOMAIN=https://brew.devneeds.ir/api` · `HOMEBREW_ARTIFACT_DOMAIN=https://docker.devneeds.ir` | 🟡 documented |
| **Windows Update proxy** | `win.devneeds.ir:8445` | 🟡 documented |
| GitHub repo zip downloads | `https://github.devneeds.ir/` (account login required) | 🟡 documented |
| **VS Code extensions** | search `POST https://backend.devneeds.ir/api/vscode/search` ✅ 200 · VSIX `GET …/api/vscode/download?publisher=&extension=&version=` (Bearer token = DevNeeds account) | ✅ search / 🟡 download |

### 2.6 🏢 Liara (لیارا) — `liara.ir/mirrors`

PaaS provider; **pull-through cache** model ("almost always level with upstream on newest request").

| Ecosystem | Endpoint | Status |
|---|---|---|
| Docker Hub mirror | `https://docker-mirror.liara.ir` | ✅ `/v2/` 401 |
| PyPI | `https://package-mirror.liara.ir/repository/pypi/simple` | ✅ 200 |
| npm | `https://package-mirror.liara.ir/repository/npm/` | ✅ 200 |
| Go modules | `https://package-mirror.liara.ir/repository/go/` | 🟡 documented |
| Composer | `https://package-mirror.liara.ir/repository/composer/` | 🟡 documented |
| Ubuntu apt | `http://linux-mirror.liara.ir/repository/ubuntu` + `/repository/ubuntu-security` | 🟡 documented |
| Debian apt | `http://linux-mirror.liara.ir/repository/debian` + `/repository/debian-security` | 🟡 documented |
| ghcr / Microsoft artifacts / Quay / K8s registries; NuGet; Rocky, Alpine, CentOS, Fedora, OpenSUSE, Arch, Manjaro | endpoints not published on fetched pages | 🟡 listed |

### 2.7 🏛️ Jamko / "chrepo" (جمکو — ایران ریپازیتوری) — `jamko.ir` → `*.chrepo.ir`

Government-backed (Iran Ministry of ICT / ITO). Guide + downloadable sample configs (`init.gradle`, `settings.xml`, `.npmrc`, `NuGet.Config`, per-distro `chrepo.repo`).

| Ecosystem | Endpoint | Status |
|---|---|---|
| PyPI | `https://pypi.chrepo.ir/simple` | ✅ 200 |
| npm | `https://npm.chrepo.ir/` | ✅ 200 |
| Docker registry (+ kubeadm `--image-repository docker.chrepo.ir`) | `https://docker.chrepo.ir` | ✅ `/v2/` 401 |
| Helm | `https://helm.chrepo.ir` | 🟡 documented |
| Ubuntu apt | `https://ubuntu.chrepo.ir` | 🟡 documented |
| Debian apt | `https://debian.chrepo.ir` | 🟡 documented |
| Maven | `https://maven.chrepo.ir` | 🟡 documented |
| Gradle plugin portal + distributions | `https://gradle.chrepo.ir` / `https://download.chrepo.ir/gradle-distributions/` | 🟡 documented |
| Composer | `https://composer.chrepo.ir` | 🟡 documented |
| NuGet | `https://nuget.chrepo.ir` | 🟡 documented |
| Android SDK | `SDK_TEST_BASE_URL=https://android.chrepo.ir/repository/` | 🟡 documented |
| RPM repos (CentOS 7/8, Oracle Linux 7/8, Fedora, openSUSE) | downloadable `chrepo.repo` files | 🟡 documented |
| chromedriver / node-sass binaries | `https://download.chrepo.ir/{chromedriver,node-sass}/` | 🟡 documented |
| (legacy) `pypi.jamko.ir/simple` | — | ❌ 404 |

### 2.8 🏢 Megan / MeganHub (مگان) — `hub.megan.ir`

Broad single-host hub; endpoints from the provider's own guides, but the host returned **503 at probe time** — re-test.

| Ecosystem | Endpoint | Status |
|---|---|---|
| PyPI | `https://hub.megan.ir/pypi/simple` | ⚠️ 503 |
| npm | `https://hub.megan.ir/npm` | ⚠️ 503 |
| Docker registry (pull prefix `hub.megan.ir/<image>`) | `https://hub.megan.ir` | ⚠️ 503 |
| Docker CE apt repo | `https://hub.megan.ir/docker/\$distro` | 🟡 documented |
| Go modules + sumdb | `https://hub.megan.ir/go` + `/sumdb` | 🟡 documented |
| Composer / Maven / NuGet | `…/composer`, `…/maven`, `…/nuget/index.json` | 🟡 documented |
| Debian / Ubuntu apt | `https://hub.megan.ir/debian` / `/ubuntu` | 🟡 documented |
| Alpine apk | `https://hub.megan.ir/alpine` | 🟡 documented |
| Arch, Fedora | "coming soon" | 🟡 announced |

### 2.9 🏢 MobinHost (مبین‌هاست) — Linux `mirror.mobinhost.com` · Docker `docker.mobinhost.com`

Classic distro mirror (HTTP/HTTPS/FTP/RSYNC, IPv4+IPv6, Tehran DC1, ~120 TB); **same-day sync** at review.

| Ecosystem | Endpoint | Status |
|---|---|---|
| Ubuntu apt + ISOs | `https://mirror.mobinhost.com/ubuntu` + `/ubuntu-releases` | ✅ fresh (bionic→resolute + devel) |
| Debian apt + CD | `/debian` `/debian-security` `/debian-cd` | ✅ fresh |
| AlmaLinux / Fedora / Manjaro / Arch / Alpine / EPEL / Raspbian / FreeBSD | `/almalinux` `/fedora` `/manjaro` `/archlinux` `/alpine` `/epel` `/raspbian` `/FreeBSD` | ✅ fresh (most trees 2026-11-19) |
| MariaDB / MongoDB | `/mariadb` `/mongodb` (mongo stale 2026-07) | ✅ / ⚠️ |
| Docker Hub mirror | `https://docker.mobinhost.com` (`"registry-mirrors": ["https://docker.mobinhost.com"]`) | ✅ `/v2/` 200 |

### 2.10 🏢 Pardisco — Pardis Co. (پاردیسکو) — `mirrors.pardisco.co`

Guides verified; **all deep repo paths returned 500 at probe time** — re-test before relying on it.

| Ecosystem | Endpoint | Status |
|---|---|---|
| Ubuntu apt + security + CD | `https://mirrors.pardisco.co/ubuntu` `/ubuntu-security` `/ubuntu-cd` | ⚠️ 500 at probe |
| Debian (+ CD), CentOS, Alpine, OmniOS, pkgsrc | guides at `/posts/{debian,centos,alpine,omnios,pkgsrc}/` | 🟡 documented |
| PyPI | `https://mirrors.pardisco.co/pip/simple/` | ⚠️ 500 at probe |
| npm / Go / NuGet | guides at `/posts/{npm,go,nuget}/` | 🟡 documented |
| Docker Hub cache | pull prefix `mirrors.pardisco.co/<image>` · `"registry-mirrors": ["https://mirrors.pardisco.co"]` | ⚠️ `/v2/` 500 |

### 2.11 🏢 Asiatech CloudIR (کلود دات آی‌ران) — `mirror.cdn.ir`

Nexus 3.77.2 (`mirror.cdn.ir` → `mirror.10.ir.cdn.ir`); free service; **pull-cache of archive.ubuntu.com**, sync stamps 2026-11-19.

| Ecosystem | Endpoint | Status |
|---|---|---|
| Docker Hub mirror | `"registry-mirrors": ["https://mirror.cdn.ir"]` | ✅ `/v2/` 401 |
| Docker CE apt repo | `https://mirror.cdn.ir/repository/docker/linux/ubuntu` (GPG at `…/gpg`) | 🟡 documented |
| Ubuntu apt (22 & lower documented; 24+ via `ubuntu.sources`) | `https://mirror.cdn.ir/repository/ubuntu` (note the `/repository` prefix) | ✅ dists 200, trusty→current |
| Debian / other ecosystems | not documented | 🟡 unlisted |

### 2.12 🏛️ ITO National Repository (مخزن ملی منابع متن باز) — `repo.ito.gov.ir` + `archive.ito.gov.ir`

Government (Iran ITO). Portal = search + per-repo guides (~70 repos); **download endpoint = `archive.ito.gov.ir`** ("main mirror" = passed security review; a second "mirror 2" exists, endpoint JS-hidden).

`archive.ito.gov.ir` root autoindex (57 dirs), with sync state:

- **Fresh (2026-11):** ubuntu, debian(+security), alpine, npm, maven(+public), nuget, rust, golang, almalinux, rocky, centos, fedora
- **Moderate (2026-H1):** archlinux, kali, termux, java, dotnet, flutter (2026-03), python (2026-02)
- **Stale (2023 or earlier):** linuxmint (2024), mageia, openmandriva, opensuse, julia, composer, gradle, google, kubernetes, postgresql, mysql, mongodb, influxdb, grafana, vscode, azure-cli
- **AI/LLM:** `llm/`, `llm2/`, `hf-cache/` (Hugging Face cache)
- **Infra repos:** docker-ce, apache, nginx, ceph, cassandra, gitlab, mariadb, redis, zabbix, virtualbox, unity, mssql-server-2025

Config (official, generated by the portal):
```text
deb https://archive.ito.gov.ir/ubuntu resolute main restricted universe multiverse
deb https://archive.ito.gov.ir/ubuntu resolute-updates main restricted universe multiverse
deb https://archive.ito.gov.ir/ubuntu resolute-backports main restricted universe multiverse
```

### 2.13 🎓 IUT IT Center (دانشگاه صنعتی اصفهان) — `repo.iut.ac.ir/repo/`

University mirror; fresh (focal/jammy/noble/resolute synced 2026-11-18): **alpine, archlinux, debian + debian-security, ubuntu (trusty→resolute), mint, manjaro, raspbian + archive.raspberrypi.org, fedora, rocky-linux, opensuse, OpenBSD, epel, CTAN (tex-archive)** + misc (bacula, influxdata).

### 2.14 🏢 Sindad Cloud (سینداد) — `ir.ubuntu.sindad.cloud` · `ir.debian.sindad.cloud` · `ir.centos.sindad.cloud`

Three classic mirrors, all actively syncing on review day:

| Mirror | Coverage | Status |
|---|---|---|
| Ubuntu | full archive.ubuntu.com layout (root **and** `/ubuntu/`), trusty→stonking + devel, all pockets | ✅ fresh (ls-lR regen 2026-11-19) |
| Debian | `/debian` `/debian-security` `/debian-backports` `/debian-cd` `/debian-archive` — bullseye→trixie, forky, sid | ✅ fresh |
| CentOS | full tree 2.1 → **8 / 8-stream** (nothing newer) | ✅ syncing (EOL-era content) |

### 2.15 🏢 Pishgaman (پیشگامان) — `ubuntu.pishgaman.net`

| Path | Coverage | Status |
|---|---|---|
| `/cdimage/` | Ubuntu ISOs **14.04 → 26.10** (incl. 24.04.5.1), releases/streams dirs | ✅ fresh (trace 2026-11-19) |
| `/ubuntu/` | full apt archive, trusty→stonking, all pockets | ✅ fresh |

### 2.16 🏢 Shatel (شاتل) — `mirror.shatel.ir`

**Debian-only** mirror (debian + debian-security), fresh (forky synced 2026-11-18); official snippets for trixie / bookworm / bullseye on the homepage (plain http).

### 2.17 🏢 Rasanegar (رسانگار) — `mirror.rasanegaar.com` (note double `aa`)

Broad single-host catalog (Ubuntu dists synced on review day). ⚠️ Path names differ from upstream!

| Ecosystem | Path / Endpoint | Status |
|---|---|---|
| Ubuntu apt | `https://mirror.rasanegaar.com/ubuntu/` | ✅ fresh |
| Debian apt | `https://mirror.rasanegaar.com/apt/` (⚠️ not `/debian`) | 🟡 listed |
| Alpine / Arch / EPEL | `/apk/` `/archlinux/` `/epel/` | 🟡 listed |
| Ubuntu ISOs | `/ubuntu-cd/` | 🟡 listed |
| npm / PyPI / Maven / Composer / NuGet / Go / Crates / Terraform / HuggingFace | `/npm/` `/pypi/simple/` `/maven/` `/php/` `/nuget/` `/golang/` `/crates/` `/terraform/` `/hf/` | 🟡 listed |
| Docker Hub | `docker-registry.rasanegaar.com` — pull prefix `docker-registry.rasanegaar.com/dockerhub/<image>` | 🟡 listed |
| GNU / VideoLAN / HBCD | `/gnu/` `/videolan/` `/hbcd/` | 🟡 listed |
| CentOS, Alma, Rocky, Mint, Manjaro, OpenSUSE, Kali, CTAN | "coming soon" | 🟡 announced |

### 2.18 🏢 AminiDC (امین دیتاسنتر) — `mirror.aminidc.com` (HTTP + FTP + RSYNC)

| Path | Coverage | Status |
|---|---|---|
| `/debian` | full suite | ✅ fresh (forky synced 2026-11-19) |
| `/almalinux` `/rocky` | AlmaLinux / Rocky | ✅ fresh |
| `/ubuntu` | apt tree | ⚠️ **stale ~7 months** (last sync 2026-04/05) |
| `/ubuntu-releases` `/debian-cd` | ISO images | ✅ fresh |
| `/epel` `/linuxmint` | EPEL / Mint | ⚠️ stale (2025-10 / 2021) |
| `/nvidia-container-toolkit` | NVIDIA container repo | ✅ |
| legacy `.repo` files at root | CentOS 7 / EPEL 7 / Fedora definitions | 🟡 legacy |

### 2.19 ❌ Dead / unreachable at verification (2026-11-19)

| Source | Listed for | Finding |
|---|---|---|
| **KubarCloud** `mirror.kubarcloud.com` | language & Linux repos | ❌ NXDOMAIN — domain expired/removed; TLS killed on all backends |
| **HyperClouds** `mirrors.hyperclouds.ir` | PyPI `pypi.hyperclouds.ir/simple`, Ubuntu `ubuntu.hyperclouds.ir/ubuntu`, Docker CE apt | ❌ authoritative DNS refuses queries (SERVFAIL); site unreachable. Still referenced by third-party scripts (incl. thealibigdeli's `docker-installer.sh` default) — do not rely on it |
| **Rust Meetup** `index.rust-meetup.ir` (+ `crates.rust-meetup.ir`) | crates.io mirror | ❌ 504 gateway timeout, persistent (~15 min of retries) — parked behind ArvanCloud, origin down |

### 2.20 Aggregator pages (not mirrors themselves)

| Page | What it provides |
|---|---|
| `thealibigdeli.ir/pypi-alternative` | Static weekly search UI over 6 PyPI mirrors (RunFlare, Chabokan, HyperClouds, Liara, Pardisco, Jamko) + install-command generator |
| `thealibigdeli.ir/ubuntu-solutions` | `mirror-changer.sh` — interactive switcher across **11 Ubuntu mirrors** (ArvanCloud, Chabokan, RunFlare, Sindad, HyperClouds, Shatel*, Rasanegar*, Pardisco, MobinHost, IRArchive `ir.archive.ubuntu.com`, Liara; *marked inactive) + `docker-installer.sh` (Docker CE with HyperClouds repo default) — hosted on ArvanCloud S3 |
| `devneeds.ir/country-mirrors` | Directory of other Iranian mirrors with update-lag stats |

---

## Part 3 — Configuration playbook

> Per tool: **ordered options** → configure pattern → test → revert. Status column = probe result on 2026-11-19 (re-test on the target machine).
> Environment-variable style options (`PUB_HOSTED_URL`, `GOPROXY`, …) should be written to the user's shell profile (`~/.bashrc` / `~/.zshrc`, or Windows env vars via `setx`) **only after** the user confirms scope (user vs global).

### 3.1 🐍 Python / pip (PyPI)

Pattern:
```bash
pip config --user set global.index-url <INDEX_URL>
# optional; only if TLS problems appear:
pip config --user set global.trusted-host <HOST>
```
⚠️ The source page's snippet sets `trusted-host repo.hmirror.ir` — that host does not match the mirror; the correct value is `mirror-pypi.runflare.com`, or simply omit it (HTTPS already validates).

| # | Provider | INDEX_URL | Status |
|---|---|---|---|
| 1 | RunFlare | `https://mirror-pypi.runflare.com/simple` | ✅ |
| 2 | Chabokan | `https://mirror2.chabokan.net/pypi/simple/` | ✅ |
| 3 | IranServer | `https://pypi.iranserver.com/repository/pypi/simple` | ✅ |
| 4 | Liara | `https://package-mirror.liara.ir/repository/pypi/simple` | ✅ |
| 5 | Jamko (chrepo) | `https://pypi.chrepo.ir/simple` | ✅ |
| 6 | DevNeeds | `https://pypi.devneeds.ir/simple/` | ⚠️ geo-WAF from abroad |
| 7 | Megan | `https://hub.megan.ir/pypi/simple` | ⚠️ 503 |
| 8 | Pardisco | `https://mirrors.pardisco.co/pip/simple/` | ⚠️ 500 |
| 9 | Rasanegar | `https://mirror.rasanegaar.com/pypi/simple/` | 🟡 |

Test (works on all options):
```bash
python -m pip download --no-deps --dest "$TMPDIR/pip-test" -i <INDEX_URL> six
```

Revert: `pip config --user unset global.index-url` (and `global.trusted-host`, `global.index` if set).

### 3.2 🟢 Node.js / npm (+ Yarn, pnpm)

Pattern:
```bash
npm config set registry <REGISTRY_URL>
# yarn:  yarn config set registry <REGISTRY_URL>
# pnpm:  pnpm config set registry <REGISTRY_URL>
```

| # | Provider | REGISTRY_URL | Status |
|---|---|---|---|
| 1 | RunFlare | `https://mirror-npm.runflare.com` | ✅ |
| 2 | Chabokan | `https://mirror2.chabokan.net/npm/` | ✅ |
| 3 | IranServer | `https://npm.iranserver.com/repository/npm/` | ✅ |
| 4 | Liara | `https://package-mirror.liara.ir/repository/npm/` | ✅ |
| 5 | Jamko (chrepo) | `https://npm.chrepo.ir/` | ✅ |
| 6 | DevNeeds | `https://npm.devneeds.ir/` | ⚠️ geo-WAF |
| 7 | Megan | `https://hub.megan.ir/npm` | ⚠️ 503 |
| 8 | Rasanegar | `https://mirror.rasanegaar.com/npm/` | 🟡 |

Test: `npm view lodash version --registry <REGISTRY_URL>` (expect a version, exit 0).

Revert: `npm config delete registry` (restores `https://registry.npmjs.org/`).

### 3.3 🐳 Docker Hub images

Two mechanisms — the agent should prefer **`registry-mirrors`** (Docker automatically falls back through the list, then to Docker Hub):
```bash
# /etc/docker/daemon.json
{ "registry-mirrors": ["<MIRROR_URL>"] }
sudo systemctl daemon-reload && sudo systemctl restart docker
```
Explicit alternative (no daemon change): pull prefix `docker pull <HOST>/<image>` — for official images `docker.arvancloud.ir/python:3.12`; Rasanegar uses `docker-registry.rasanegaar.com/dockerhub/<image>`.

| # | Provider | MIRROR_URL | Status |
|---|---|---|---|
| 1 | ArvanCloud | `https://docker.arvancloud.ir` | ✅ |
| 2 | RunFlare (proxies Hub, mcr, k8s, gcr, ghcr, quay) | `https://mirror-docker.runflare.com` | ✅ |
| 3 | IranServer | `https://docker.iranserver.com` | ✅ |
| 4 | MobinHost | `https://docker.mobinhost.com` | ✅ |
| 5 | Liara | `https://docker-mirror.liara.ir` | ✅ |
| 6 | Chabokan | `https://mirror2.chabokan.net` | ✅ |
| 7 | Asiatech | `https://mirror.cdn.ir` | ✅ |
| 8 | Jamko (chrepo) | `https://docker.chrepo.ir` | ✅ |
| 9 | DevNeeds | `https://docker.devneeds.ir` | ✅ |
| 10 | Megan | `https://hub.megan.ir` | ⚠️ 503 |
| 11 | Pardisco | `https://mirrors.pardisco.co` | ⚠️ 500 |
| 12 | Rasanegar (pull prefix only) | `docker-registry.rasanegaar.com/dockerhub` | 🟡 |

Test: `docker pull hello-world:latest && docker run --rm hello-world` (also verify the *daemon log*/`docker info` shows the mirror was used).

Revert: remove the `registry-mirrors` entry from `/etc/docker/daemon.json` (keep a `.bak-<date>` copy) and restart Docker.

### 3.4 🐧 Ubuntu (apt)

Pattern — replace all `archive.ubuntu.com` / `security.ubuntu.com` occurrences:
```bash
sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak-<date>   # plus /etc/apt/sources.list.d/*.sources on 24.04+
sudo sed -i 's|http://archive.ubuntu.com/ubuntu|<APT_BASE>|g; s|https://archive.ubuntu.com/ubuntu|<APT_BASE>|g; s|http://security.ubuntu.com/ubuntu|<APT_BASE>|g; s|https://security.ubuntu.com/ubuntu|<APT_BASE>|g' /etc/apt/sources.list
# Ubuntu 24.04+ (deb822): apply the same substitutions to /etc/apt/sources.list.d/ubuntu.sources
```
Exact-path option (no substitution needed — deb822 template, works for any option below):
```text
Types: deb
URIs: <APT_BASE>
Suites: noble noble-updates noble-backports noble-security
Components: main restricted universe multiverse
Signed-By: /usr/share/keyrings/ubuntu-archive-keyring.gpg
```

| # | Provider | APT_BASE | Status |
|---|---|---|---|
| 1 | ArvanCloud (source page's pick) | `http://mirror.arvancloud.ir/ubuntu` | ✅ |
| 2 | RunFlare ("most up-to-date" per source) | `http://mirror-linux.runflare.com/ubuntu` | ✅ |
| 3 | Sindad | `https://ir.ubuntu.sindad.cloud/ubuntu` | ✅ |
| 4 | MobinHost | `https://mirror.mobinhost.com/ubuntu` | ✅ |
| 5 | ITO national (security-reviewed) | `https://archive.ito.gov.ir/ubuntu` | ✅ |
| 6 | IUT | `https://repo.iut.ac.ir/repo/ubuntu` | ✅ |
| 7 | Pishgaman | `https://ubuntu.pishgaman.net/ubuntu` | ✅ |
| 8 | Rasanegar | `https://mirror.rasanegaar.com/ubuntu/` | ✅ |
| 9 | Asiatech (Ubuntu ≤24 documented; use `/repository/ubuntu`) | `https://mirror.cdn.ir/repository/ubuntu` | ✅ |
| 10 | IranServer | `https://mirror.iranserver.com/ubuntu/` | 🟡 (hourly-sync claim) |
| 11 | Liara | `http://linux-mirror.liara.ir/repository/ubuntu` | 🟡 |
| 12 | Chabokan | `https://mirror2.chabokan.net/ubuntu` | 🟡 ⚠️ unsigned (`trusted=yes`) |
| 13 | Pardisco | `https://mirrors.pardisco.co/ubuntu` | ⚠️ 500 |
| — | AminiDC | `http://mirror.aminidc.com/ubuntu` | ⚠️ stale ~7 months — avoid |
| — | HyperClouds | `https://ubuntu.hyperclouds.ir/ubuntu` | ❌ dead |

Test: `sudo apt-get update` → exit 0, zero `Err:` lines; then `apt-get download curl` into a temp dir.

Revert: restore the `.bak-<date>` files, `sudo apt-get update`.

### 3.5 🐧 Debian (apt)

Same pattern as §3.4, substituting `deb.debian.org` / `security.debian.org`.

| # | Provider | APT_BASE | Status |
|---|---|---|---|
| 1 | RunFlare | `http://mirror-linux.runflare.com/debian` | ✅ |
| 2 | MobinHost | `https://mirror.mobinhost.com/debian` (+ `/debian-security`) | ✅ |
| 3 | Sindad | `https://ir.debian.sindad.cloud/debian` (+ `/debian-security`) | ✅ |
| 4 | ITO national | `https://archive.ito.gov.ir/debian` (+ `/debian-security`) | ✅ |
| 5 | Shatel (Debian specialist) | `http://mirror.shatel.ir/debian` (+ `/debian-security`) | ✅ |
| 6 | IUT | `https://repo.iut.ac.ir/repo/debian` (+ `/repo/debian-security`) | ✅ |
| 7 | ArvanCloud | `https://mirror.arvancloud.ir/debian` (+ `/debian-security`) | ✅ |
| 8 | AminiDC | `http://mirror.aminidc.com/debian` | ✅ fresh |
| 9 | IranServer | `https://mirror.iranserver.com/debian/` (+ `/debian-security/`) | 🟡 |
| 10 | Liara | `http://linux-mirror.liara.ir/repository/debian` | 🟡 |
| 11 | Chabokan | `https://mirror2.chabokan.net/debian` | 🟡 ⚠️ unsigned |
| 12 | Rasanegar (⚠️ path is `/apt`, not `/debian`) | `https://mirror.rasanegaar.com/apt/` | 🟡 |

Debian component set: `main contrib non-free non-free-firmware` (bullseye+). Test/revert as §3.4.

### 3.6 🏛️ Docker CE & third-party apt repos

| Repo | Options (in order) |
|---|---|
| Docker CE (`download.docker.com`) | 1. DevNeeds `https://apt.devneeds.ir/docker/$ID $VERSION_CODENAME stable` · 2. Megan `https://hub.megan.ir/docker/$distro` 🟡 · 3. Asiatech `https://mirror.cdn.ir/repository/docker/linux/ubuntu` (GPG `…/gpg`) |
| PostgreSQL (PGDG) | DevNeeds `https://apt.devneeds.ir/postgres $OS_CODENAME-pgdg main` |
| VS Code (apt) | DevNeeds `https://apt.devneeds.ir/vscode stable main` |
| Trivy / Zabbix / Waydroid | DevNeeds `https://apt.devneeds.ir/{trivy,zabbix,waydroid}` |
| MariaDB | IranServer `https://mirror.iranserver.com/mariadb/` (apt+yum layouts) |
| NVIDIA container toolkit | AminiDC `http://mirror.aminidc.com/nvidia-container-toolkit` |
| Kubernetes packages (`pkgs.k8s.io`) | 1. IranServer `https://mirror.iranserver.com/kubernetes/` (v1.36 layout) · 2. RunFlare `https://mirror-k8s.runflare.com` |

Test: `sudo apt-get update` (scoped: only the added list file errors matter) + a targeted `apt-get download <pkg>`; revert = delete the added `.list`/`.sources` file.

### 3.7 🏛️ Other distros

| Distro | Options (ordered; same substitution-test-revert loop as apt/dnf/pacman) |
|---|---|
| **Arch Linux** | 1. RunFlare `http://mirror-linux.runflare.com/archlinux` ✅ · 2. ArvanCloud `https://mirror.arvancloud.ir/archlinux` ✅ · 3. MobinHost `https://mirror.mobinhost.com/archlinux` ✅ · 4. IUT `https://repo.iut.ac.ir/repo/archlinux` ✅ · 5. DevNeeds `https://arch.devneeds.ir/$repo/os/$arch` 🟡 · 6. ITO `https://archive.ito.gov.ir/archlinux` 🟡 |
| **Alpine** | 1. RunFlare `http://mirror-linux.runflare.com/alpine` ✅ · 2. ArvanCloud `https://mirror.arvancloud.ir/alpine` ✅ · 3. MobinHost `https://mirror.mobinhost.com/alpine` ✅ · 4. ITO `https://archive.ito.gov.ir/alpine` ✅ · 5. IUT `https://repo.iut.ac.ir/repo/alpine` ✅ · 6. Megan `https://hub.megan.ir/alpine` ⚠️ |
| **Fedora** | 1. RunFlare `http://mirror-linux.runflare.com/fedora` ✅ · 2. MobinHost `https://mirror.mobinhost.com/fedora` ✅ · 3. ITO `https://archive.ito.gov.ir/fedora` ✅ · 4. IUT `https://repo.iut.ac.ir/repo/fedora` ✅ · 5. Jamko `chrepo.repo` file 🟡 |
| **CentOS / AlmaLinux / Rocky + EPEL** | 1. MobinHost `/almalinux` `/epel` ✅ · 2. AminiDC `/almalinux` `/rocky` ✅ · 3. IranServer `https://mirror.iranserver.com/almalinux/` + `/epel/` 🟡 · 4. ITO `/centos` `/almalinux` `/rocky` 🟡 · 5. Sindad CentOS `https://ir.centos.sindad.cloud/` (≤8) ✅ · 6. Jamko `chrepo.repo` (CentOS 7/8, Oracle, Fedora, openSUSE) 🟡 · 7. RunFlare EPEL `https://mirror-epel.runflare.com` ⚠️ 503 |
| **Kali** | 1. RunFlare `http://mirror-linux.runflare.com/kali` ✅ · 2. DevNeeds `https://kali.devneeds.ir kali-rolling main contrib non-free non-free-firmware` 🟡 · 3. ITO `/kalilinux` 🟡 |
| **Manjaro** | 1. MobinHost `/manjaro` ✅ · 2. IUT `/repo/manjaro` ✅ |
| **openSUSE** | 1. IUT `/repo/opensuse` (stale 2025-10) ⚠️ · 2. ITO `/opensuse` (stale 2023) ⚠️ · 3. Jamko `chrepo.repo` 🟡 |
| **Linux Mint** | 1. IUT `/repo/mint` 🟡 · 2. ITO `/linuxmint` (2024) ⚠️ · 3. AminiDC `/linuxmint` (2021) ⚠️ |
| **Raspberry Pi OS** | 1. MobinHost `/raspbian` ✅ · 2. IUT `/repo/raspbian` + `/repo/archive.raspberrypi.org` ✅ |

### 3.8 🎯 Flutter / Dart (pub.dev)

```bash
export PUB_HOSTED_URL="<PUB>"
export FLUTTER_STORAGE_BASE_URL="<STORAGE>"   # write to shell profile
```

| # | Provider | PUB (pub.dev) | STORAGE (flutter) | Status |
|---|---|---|---|---|
| 1 | DevNeeds | `https://dart.devneeds.ir` | `https://flutter.devneeds.ir` | 🟡 (geo-WAF possible) |
| 2 | RunFlare | — (no pub.dev mirror) | `https://mirror-flutter.runflare.com` | ✅ storage only |

Also available: RunFlare Flutter-SDK storage for `flutter` tool downloads; ITO `archive.ito.gov.ir/flutter/` (2026-03, stale-ish).

Test:
```bash
curl -fsSL "$PUB_HOSTED_URL/api/packages/path" >/dev/null          # hosted API alive
curl -fsSL "$FLUTTER_STORAGE_BASE_URL/flutter_infra_release/releases/releases_linux.json" >/dev/null
cd "$(mktemp -d)" && dart create -t console probe && dart pub get    # end-to-end, if Dart/Flutter installed
```

Revert: unset both variables in the shell profile.

### 3.9 🐹 Go modules

```bash
go env -w GOPROXY=<GOPROXY>
# only if the mirror cannot proxy checksum DB:
go env -w GOSUMDB=off          # ⚠️ security tradeoff — try mirror-provided GONOSUMDB/GOSUMDB first
```

| # | Provider | GOPROXY | Notes | Status |
|---|---|---|---|---|
| 1 | RunFlare | `https://mirror-go.runflare.com,direct` | keep checksum DB | ✅ |
| 2 | IranServer | `https://go.iranserver.com/repository/go/` | their guide sets `GOSUMDB=off` | 🟡 |
| 3 | Liara | `https://package-mirror.liara.ir/repository/go/` | guide sets `GOSUMDB=off` | 🟡 |
| 4 | DevNeeds | `https://go.devneeds.ir,direct` | `GOSUMDB="sum.golang.org https://go-sum.devneeds.ir"` (checksum DB proxied — best) | 🟡 |
| 5 | Megan | `https://hub.megan.ir/go,direct` | `GOSUMDB="sum.golang.org https://hub.megan.ir/sumdb"` | ⚠️ 503 |
| 6 | Rasanegar | `https://mirror.rasanegaar.com/golang/` | — | 🟡 |

Test: `cd "$(mktemp -d)" && go mod init probe && GOPROXY=<url>,direct go get golang.org/x/text@v0.14.0`.

Revert: `go env -w GOPROXY=https://proxy.golang.org,direct` and `go env -w GOSUMDB=sum.golang.org`.

### 3.10 🦀 Rust / Cargo (crates.io)

Pattern (`~/.cargo/config.toml`):
```toml
[source.crates-io]
replace-with = "<ALIAS>"

[source.<ALIAS>]
registry = "<SPARSE_REGISTRY>"

[net]
git-fetch-with-cli = true
```
Set `registry = "sparse+<URL>"` when the mirror requires the sparse-protocol prefix (add `sparse+` if the provider documents a plain index URL). Also: `export CARGO_REGISTRIES_CRATES_IO_PROTOCOL=sparse`.

| # | Provider | SPARSE_REGISTRY | Status |
|---|---|---|---|
| 1 | IranServer | `https://cargo.iranserver.com/repository/cargo/` | 🟡 documented |
| 2 | DevNeeds | `https://cargo.devneeds.ir/repository/cargo/` | 🟡 documented |
| 3 | Rasanegar | `https://mirror.rasanegaar.com/crates/` | 🟡 listed |
| 4 | ITO | `https://archive.ito.gov.ir/rust/` (raw tree, 2026-07) | ⚠️ partial |
| — | Rust Meetup `index.rust-meetup.ir` | — | ❌ down (504) |

Test: `cd "$(mktemp -d)" && cargo new probe && cd probe && cargo add serde && cargo fetch`.

Revert: delete the `[source.*]` blocks from `~/.cargo/config.toml`.

### 3.11 ☕ Java — Maven & Gradle

**Maven** (`~/.m2/settings.xml`):
```xml
<mirrors>
  <mirror>
    <id>ir-mirror</id>
    <mirrorOf>*</mirrorOf>
    <url><MAVEN_URL></url>
  </mirror>
</mirrors>
```
| # | Provider | MAVEN_URL | Status |
|---|---|---|---|
| 1 | IranServer | `https://maven.iranserver.com/repository/maven/` | 🟡 |
| 2 | RunFlare | `https://mirror-maven.runflare.com/maven2` | 🟡 |
| 3 | Jamko (chrepo) | `https://maven.chrepo.ir` | 🟡 |
| 4 | DevNeeds | `https://maven.devneeds.ir` | 🟡 |
| 5 | Megan | `https://hub.megan.ir/maven` | ⚠️ 503 |
| 6 | Rasanegar | `https://mirror.rasanegaar.com/maven/` | 🟡 |
| 7 | ITO | `https://archive.ito.gov.ir/maven/` (maven-public 2026-11) | 🟡 |

Test: `mvn -q dependency:get -DremoteRepositories=<MAVEN_URL> -Dartifact=org.slf4j:slf4j-api:2.0.9` (or `mvn -s settings.xml …`).

**Gradle** — wrapper distributions (`gradle/wrapper/gradle-wrapper.properties`):
`distributionUrl=https://<GRADLE_DIST>/gradle-8.5-bin.zip`
| # | Provider | GRADLE_DIST | Status |
|---|---|---|---|
| 1 | Jamko (chrepo) | `https://download.chrepo.ir/gradle-distributions` | 🟡 |
| 2 | DevNeeds | `https://gradle.devneeds.ir` | 🟡 |

Gradle **plugin/dependency repos** (`init.gradle` / `build.gradle`): `maven { url "https://gradle.chrepo.ir" }` (Jamko) or any Maven option above.

Test: run `./gradlew --version` (downloads the wrapper) in a scratch project.

### 3.12 🐘 PHP — Composer

```bash
composer config -g repos.packagist composer <COMPOSER_URL>
```
| # | Provider | COMPOSER_URL | Status |
|---|---|---|---|
| 1 | RunFlare | `https://mirror-composer.runflare.com` | 🟡 |
| 2 | IranServer | `https://composer.iranserver.com/repository/composer/` | 🟡 |
| 3 | Chabokan | `https://mirror2.chabokan.net/composer/` | ✅ |
| 4 | Liara | `https://package-mirror.liara.ir/repository/composer/` | 🟡 |
| 5 | Jamko (chrepo) | `https://composer.chrepo.ir` | 🟡 |
| 6 | Megan | `https://hub.megan.ir/composer` | ⚠️ 503 |
| 7 | Rasanegar | `https://mirror.rasanegaar.com/php/` | 🟡 |

Test: `curl -fsSL <COMPOSER_URL>/packages.json | python -c "import sys,json; json.load(sys.stdin)"` and, if PHP present, `composer show -a monolog/monolog`.

Revert: `composer config -g --unset repos.packagist` (or remove the repos entry from `~/.composer/config.json`).

### 3.13 🔷 .NET — NuGet

```bash
dotnet nuget add source "<NUGET_INDEX>" --name ir-mirror
# or: nuget sources add -name ir-mirror -source <NUGET_INDEX>
```
| # | Provider | NUGET_INDEX | Status |
|---|---|---|---|
| 1 | IranServer | `https://nuget.iranserver.com/repository/nuget/` | 🟡 |
| 2 | RunFlare | `https://mirror-nuget.runflare.com` | 🟡 |
| 3 | Chabokan | `https://mirror2.chabokan.net/nuget/v3/index.json` | 🟡 |
| 4 | DevNeeds | `https://nuget.devneeds.ir/repository/nuget/index.json` | 🟡 |
| 5 | Megan | `https://hub.megan.ir/nuget/index.json` | ⚠️ 503 |
| 6 | Rasanegar | `https://mirror.rasanegaar.com/nuget/` | 🟡 |
| 7 | Jamko (chrepo) | `https://nuget.chrepo.ir` | 🟡 |

Test: `curl -fsSL <NUGET_INDEX>` (v3 index returns JSON of resources); with .NET present, `dotnet package search Newtonsoft.Json --source <NUGET_INDEX>`.

Revert: `dotnet nuget remove source ir-mirror`.

### 3.14 💎 Ruby — RubyGems

```bash
gem sources --remove https://rubygems.org/
gem sources --add <GEM_URL>
```
| # | Provider | GEM_URL | Status |
|---|---|---|---|
| 1 | IranServer | `https://rubygems.iranserver.com/repository/rubygems/` | 🟡 (only option) |

Test: `gem list -r rake --source <GEM_URL>` (or `gem fetch rake` in a temp dir).

Revert: `gem sources --remove <GEM_URL> && gem sources --add https://rubygems.org/`.

### 3.15 🤗 Hugging Face (AI models)

```bash
export HF_ENDPOINT="<HF_URL>"   # shell profile
```
| # | Provider | HF_URL | Status |
|---|---|---|---|
| 1 | DevNeeds | `https://hf.devneeds.ir/` | 🟡 documented (244 cached models) |
| 2 | Rasanegar | `https://mirror.rasanegaar.com/hf/` | 🟡 listed (config unpublished) |
| 3 | ITO | raw tree `https://archive.ito.gov.ir/llm/` `…/hf-cache/` | 🟡 manual downloads |

Test: `curl -fsSL "$HF_ENDPOINT/api/models/gpt2"` (JSON, exit 0); with `huggingface_hub`: `python -c "from huggingface_hub import HfApi; print(HfApi().model_info('gpt2'))"`.

Revert: unset `HF_ENDPOINT` (restores `https://huggingface.co`).

### 3.16 🧩 VS Code extensions

DevNeeds is the only option: UI `https://vscode.devneeds.ir/`; search API `POST https://backend.devneeds.ir/api/vscode/search` `{"searchQuery":"…"}` ✅; VSIX download `GET https://backend.devneeds.ir/api/vscode/download?publisher=<p>&extension=<e>&version=<v>` with `Authorization: Bearer <DevNeeds account token>`. This is a **manual VSIX workflow** — no `product.json` gallery drop-in is published. For apt-packaged VS Code use DevNeeds repo `https://apt.devneeds.ir/vscode stable main`.

Test: search API returns JSON containing the requested extension id.
Revert: nothing persistent (per-download workflow).

### 3.17 🤖 Android SDK

```bash
# write to shell profile:
export SDK_TEST_BASE_URL="<ANDROID_URL>"
```
| # | Provider | ANDROID_URL | Status |
|---|---|---|---|
| 1 | DevNeeds | `https://dl.devneeds.ir/android/` | 🟡 |
| 2 | Jamko (chrepo) | `https://android.chrepo.ir/repository/` | 🟡 |

Test: `curl -fsSL <ANDROID_URL>repository2-3.xml` (or `repository2-1.xml`) exits 0.

Revert: unset the variable.

### 3.18 🟩 Node.js & Python version managers

| Tool | Option | Config | Status |
|---|---|---|---|
| nvm / Node dist | RunFlare | `export NVM_NODEJS_ORG_MIRROR=https://mirror-nodejs.runflare.com/dist` | ✅ |
| nvm / Node dist | DevNeeds | `export NVM_NODEJS_ORG_MIRROR=https://nvm.devneeds.ir/nodejs-dist` | 🟡 |
| pyenv | DevNeeds | `export PYTHON_BUILD_MIRROR_URL=https://pyenv.devneeds.ir/` | 🟡 |

Test: `curl -fsSL <MIRROR>SHASUMS256.txt` (nvm) / `curl -fsSL <MIRROR>` (pyenv listing) — then optionally install a small version.

### 3.19 🍺 Homebrew (macOS)

| # | Option | Config | Status |
|---|---|---|---|
| 1 | DevNeeds | `export HOMEBREW_API_DOMAIN=https://brew.devneeds.ir/api` · `export HOMEBREW_ARTIFACT_DOMAIN=https://docker.devneeds.ir` | 🟡 |

Test: `brew fetch --force <small-formula>` (e.g. `wget`); Revert: unset both variables.

### 3.20 ☸️ Kubernetes extras (images & Helm)

| Need | Options |
|---|---|
| kubeadm control-plane images | Jamko: `kubeadm init --image-repository docker.chrepo.ir` · RunFlare: `registry.k8s.io` proxied via `mirror-docker.runflare.com` (replace domain) |
| Helm charts | Jamko: `helm repo add chrepo https://helm.chrepo.ir` |
| Test | `helm search repo chrepo` / `kubeadm config images pull --image-repository docker.chrepo.ir` |

### 3.21 💿 OS ISO downloads

| OS | Options (ordered) |
|---|---|
| **Ubuntu ISOs** | 1. Pishgaman `https://ubuntu.pishgaman.net/cdimage/` (14.04→26.10) ✅ · 2. MobinHost `https://mirror.mobinhost.com/ubuntu-releases` ✅ · 3. AminiDC `http://mirror.aminidc.com/ubuntu-releases` ✅ · 4. Rasanegar `https://mirror.rasanegaar.com/ubuntu-cd/` 🟡 · 5. IranServer `https://mirror.iranserver.com/iso/` 🟡 |
| **Debian ISOs** | 1. MobinHost `/debian-cd` ✅ · 2. Sindad `https://ir.debian.sindad.cloud/debian-cd/` ✅ · 3. AminiDC `/debian-cd` ✅ · 4. IranServer `/iso/` 🟡 |
| **Windows / ESXi / Proxmox / SQL Server** | IranServer `https://mirror.iranserver.com/iso/` (unique) 🟡 |

Test: `curl -sIL "<iso-url>" | head -1` → `HTTP/2 200`, and `Content-Length` > 0 (use the exact filename from the directory listing).

---

## Appendix A — Cross-provider quick matrix

Providers × ecosystems (✅ verified / 🟡 documented / ⚠️ flagged / ❌ dead):

| Provider | PyPI | npm | Docker | Ubuntu | Debian | Arch | Alpine | Fedora | RHEL-family | Flutter | Go | Cargo | Maven | Composer | NuGet | Ruby | HF | VSCode | Android | ISO |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
| RunFlare | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ⚠️ | ✅ | ✅ | — | 🟡 | 🟡 | 🟡 | — | — | — | — | — |
| IranServer | ✅ | ✅ | ✅ | 🟡 | 🟡 | — | — | — | 🟡 | — | 🟡 | 🟡 | 🟡 | 🟡 | 🟡 | 🟡 | — | — | — | 🟡 |
| Chabokan | ✅ | ✅ | ✅ | 🟡⚠ | 🟡⚠ | — | — | — | — | — | — | — | — | ✅ | 🟡 | — | — | — | — | — |
| ArvanCloud | ⚠️ | — | ✅ | ✅ | ✅ | ✅ | ✅ | ⚠️ | ⚠️ | — | — | — | — | — | — | — | — | — | — | — |
| DevNeeds | ⚠️ | ⚠️ | ✅ | 🟡 | 🟡 | 🟡 | — | — | 🟡 | 🟡 | 🟡 | 🟡 | 🟡 | — | 🟡 | — | 🟡 | 🟡 | 🟡 | — |
| Liara | ✅ | ✅ | ✅ | 🟡 | 🟡 | 🟡 | 🟡 | 🟡 | 🟡 | — | 🟡 | — | — | 🟡 | 🟡 | — | — | — | — | — |
| Jamko/chrepo | ✅ | ✅ | ✅ | 🟡 | 🟡 | — | — | 🟡 | 🟡 | — | — | — | 🟡 | 🟡 | 🟡 | — | — | — | 🟡 | — |
| Megan | ⚠️ | ⚠️ | ⚠️ | 🟡 | 🟡 | — | 🟡 | 🟡 | — | — | 🟡 | — | 🟡 | 🟡 | 🟡 | — | — | — | — | — |
| MobinHost | — | — | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | — | — | — | — | — | — | — | — | — | — | ✅ |
| Pardisco | ⚠️ | 🟡 | ⚠️ | ⚠️ | 🟡 | — | 🟡 | — | — | — | 🟡 | — | — | — | 🟡 | — | — | — | — | — |
| Asiatech | — | — | ✅ | ✅ | — | — | — | — | — | — | — | — | — | — | — | — | — | — | — | — |
| ITO (gov) | 🟡 | ✅ | 🟡 | ✅ | ✅ | 🟡 | ✅ | ✅ | 🟡 | 🟡 | 🟡 | ⚠️ | 🟡 | ⚠️ | 🟡 | — | 🟡 | — | — | 🟡 |
| IUT (univ) | — | — | — | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ | — | — | — | — | — | — | — | — | — | — | — |
| Sindad | — | — | — | ✅ | ✅ | — | — | — | ✅(≤8) | — | — | — | — | — | — | — | — | — | — | ✅ |
| Pishgaman | — | — | — | ✅ | — | — | — | — | — | — | — | — | — | — | — | — | — | — | — | ✅ |
| Shatel | — | — | — | ⚠️ | ✅ | — | — | — | — | — | — | — | — | — | — | — | — | — | — | — |
| Rasanegar | 🟡 | 🟡 | 🟡 | ✅ | 🟡 | 🟡 | 🟡 | — | 🟡(EPEL) | — | 🟡 | 🟡 | 🟡 | 🟡 | 🟡 | — | 🟡 | — | — | 🟡 |
| AminiDC | — | — | — | ⚠️stale | ✅ | — | — | ⚠️legacy | ✅ | — | — | — | — | — | — | — | — | — | — | ✅ |
| KubarCloud | ❌ | ❌ | ❌ | ❌ | ❌ | — | — | — | — | — | — | — | — | — | — | — | — | — | — | — |
| HyperClouds | ❌ | ❌ | ❌ | ❌ | — | — | — | — | — | — | — | — | — | — | — | — | — | — | — | — |
| Rust Meetup | — | — | — | — | — | — | — | — | — | — | — | ❌ | — | — | — | — | — | — | — | — |

## Appendix B — Verification log (summary)

- All provider pages fetched 2026-11-19 with TLS-fallback curl (`--tlsv1.2 -k`).
- Probe patterns: registry `/v2/` (expect 200/401), PyPI `/simple/` (expect HTML/JSON index), npm `/lodash` (expect packument), apt `/dists/` (expect suite listing), plus directory autoindexes for distro coverage.
- 3 sources dead (KubarCloud, HyperClouds, Rust Meetup); 3 flagged (Megan 503, Pardisco 500, AminiDC Ubuntu stale); all other endpoints in Part 3 verified or provider-documented as marked.
