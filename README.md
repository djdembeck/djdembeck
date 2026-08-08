## Hi, I'm David.

Software engineer at [Laxamentum Technologies](https://laxamentum.tech). I build backend systems and infrastructure — and, increasingly, the AI tooling that builds them with me. I value privacy and speed above pretty much everything else, so nearly everything I run is self-hosted and local-first.

### Lately: AI agents, all the way down

Most of my work now runs through agentic workflows I've built, tuned, and dogfooded:

- **[Mira](https://github.com/djdembeck/mira)** — self-hosted AI code review for GitHub, GitLab, and Forgejo. A full-repo index gives the reviewer real project context beyond the diff, a feedback loop learns review rules from human corrections, and OSV.dev scans watch dependencies. It reviews the PRs across my repos and our org's.
- **[oh-my-pi](https://github.com/djdembeck/oh-my-pi)** — the coding-agent harness I use and hack on daily (recent work: first-class Forgejo support). It runs `roboomp`, a triage bot that classifies incoming issues, reproduces bugs in isolated worktrees, writes the fix, and opens a PR — repro, cause, fix, verification included. I file an issue; a PR shows up.
- **[AxonHub](https://github.com/looplj/axonhub)** — the open-source LLM gateway all of this routes through. I'm the most active contributor outside the maintainer.

The model mix rotates constantly — that is the point of the gateway — but the pattern is stable: open-weight models do essentially all the work. Qwen, Kimi, GLM, DeepSeek, and MiniMax carry the agent workloads; GPT gets the occasional call, begrudgingly; self-hosted models (Gemma, Qwen — served over vLLM, SGLang, and llama.cpp) handle anything that shouldn't leave the building.

<details>
<summary>Nerd stats — since I flipped the gateway on</summary>

- **~60B** tokens routed
- **1.67M** requests — with a 100% success rate over the last 30 days
- Dozens of models in active rotation across every major open-weight family

</details>

This is how a release I'd been building toward for years finally started moving at the pace it deserved.

### Building: AudiobookDB

**[AudiobookDB](https://audiobookdb.org)** is a community-maintained audiobook metadata database — a proper separation of books and releases, moderated contributions, and fast search. Closed-source, but the site is live and growing. Go/Chi/Ent + PostgreSQL on the back, SvelteKit 5 on the front, Typesense underneath. 900+ PRs deep, most of them landed with the agent workflow above. It's the successor to my earlier [audnexus](https://github.com/laxamentumtech/audnexus) metadata API (210+ stars), and sits alongside [bragibooks](https://github.com/djdembeck/bragibooks) (200+ stars — audiobook library cleanup, itself mid-rewrite to Go + SvelteKit) and [m4b-merge](https://github.com/djdembeck/m4b-merge) (90+ stars — a Rust CLI for merging audiobooks into M4B).

### Local inference

An RTX 6000 Pro (96 GB) handles local LLM inference — for privacy, reliability, tuning headroom, and speed. vLLM, SGLang, and llama.cpp serve the models; a [custom Go router](https://github.com/djdembeck/llm-router-go) sits in front doing GPU-aware admission control and tiered routing. TTS, image generation, and embeddings run locally too.

When I do rent GPUs:

- **[NeuralWatt](https://portal.neuralwatt.com/auth/register?ref=NW-DAVID-WVH1)** (referral) — my primary cloud provider. Professional operation, support answers near 24/7. Their recent pricing change isn't my favorite and their energy efficiency is still a work in progress, but the reliability earns the slot.
- **[Synthetic](https://synthetic.new/?referral=B7fAqz37THN23mS)** (referral) — founding member, one pack. Good people; reliability and support responsiveness have been rough, so it's not my daily driver.
- **[NanoGPT](https://nano-gpt.com/r/NeDEp3UR)** (referral) — new-model testing, niche models, and a catch-all backup.

### Homelab

17+ nodes: a Raspberry Pi 5 cluster, Proxmox LXCs, and an Unraid box with the GPU. Everything deploys on git push — Docker Compose rolls out across the fleet via self-hosted CI. Traefik for ingress, OIDC for SSO, Borg backups encrypted to three locations, SOPS/age for secrets, distributed MinIO across the Pis.

My personal Forgejo instance hosts the private projects where a large share of my daily commits land, and I put my code where my mouth is: I contributed Forgejo support to Mira and [Kodus](https://github.com/djdembeck/kodus-ai) (my code reviewer before Mira), hardened it in roboomp, and my own tools ship with it from day one.

If a tool I need doesn't exist, I build it: [annalist](https://github.com/djdembeck/annalist) (AI-generated release notes from git webhooks), [llm-router-go](https://github.com/djdembeck/llm-router-go) (the GPU router above), [mira-pr-tools](https://github.com/djdembeck/mira-pr-tools), [forgejo-cli](https://github.com/djdembeck/forgejo-cli). The org's CI runners live on my hardware, its reviews run on my automation — filling gaps in the stack is half the fun.

### The stack

- **Languages:** Go, TypeScript, Python, Rust, SQL
- **Frameworks:** SvelteKit, FastAPI, Chi, Ent
- **Infrastructure:** Docker, Proxmox, Unraid, Traefik, PostgreSQL, Redis, Typesense, MinIO, Forgejo
- **AI:** vLLM, SGLang, llama.cpp, AxonHub, anything OpenAI-compatible

### Off-duty

- **Motorcycles:** Nice weather means I'm off the computer. I ride a Kawasaki ZX6R and ZX10R.
- **Fitness:** Former Yoga Sculpt instructor. Still train hard, but traded the mat for the saddle.
- **Plex:** Technically a "Plex Ninja," now just a power user.
- **Life:** Hanging out with my dog, Leah 🐶.

---

I got into software because of bugs other people missed and never fixed. That turned into a stubborn attention to detail: nothing is ever truly perfect, but software should work the way you expect it to. Most of what I build — at Laxamentum or on my own — exists because the tool I needed either didn't exist or didn't meet that bar.

I like hard infrastructure problems, lean systems, and software that respects its users. If you're building something along those lines, I'm always open to a conversation.
