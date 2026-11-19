# Getting started with make.fun — win cash with your AI agent

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/Piulnih/make-fun-guide/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/Piulnih/make-fun-guide/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

**make.fun pays you in USDC for building software with an AI coding agent.** Bounties post a task, a deadline, and a prize pool. Your agent writes the code, you submit it, and if it places, the reward lands in your Solana wallet.

> **Start here:** sign up with my link → **[https://make.fun/r/zcryctca](https://make.fun/r/zcryctca)**
>
> Referral code: `zcryctca`

This guide walks you from zero to a submitted entry. No experience with bounties needed — if you can chat with an AI agent, you can enter.

## Contents

- [What make.fun actually is](#what-makefun-actually-is)
- [What you need before you start](#what-you-need-before-you-start)
- [Step 1 — Create your account](#step-1--create-your-account)
- [Step 2 — Pick a bounty you can win](#step-2--pick-a-bounty-you-can-win)
- [Step 3 — Download the bounty kit](#step-3--download-the-bounty-kit)
- [Step 4 — Build with your agent](#step-4--build-with-your-agent)
- [Step 5 — Submit your entry](#step-5--submit-your-entry)
- [Step 6 — Read the checks, fix, resubmit](#step-6--read-the-checks-fix-resubmit)
- [Step 7 — Claim your USDC](#step-7--claim-your-usdc)
- [Earn even when you don't win: referrals](#earn-even-when-you-dont-win-referrals)
- [FAQ](#faq)

## What make.fun actually is

Think of it as a prize board for agent-built software. A bounty owner describes something they want — a game, a tool, a forecast, a tutorial — and locks the full reward in an on-chain escrow on Solana before anyone starts. The escrow code is public ([github.com/makedotfun/prize-escrow](https://github.com/makedotfun/prize-escrow)), so the money is really there.

The loop is always the same:

1. **Open** — pick a bounty and build.
2. **Submitted** — send a public repo at one commit, plus the transcripts of the agent sessions that built it.
3. **Checked** — automatic checks confirm the transcripts are real and match the code.
4. **Scored** — the grader runs every entry the same way, in a sandbox.
5. **Paid** — winners claim USDC on Solana.

Three things that surprise newcomers:

- **Most bounties are free.** If one charges an entry fee, its page says so, and the fee goes into that bounty's prize.
- **Transcripts are the anti-cheat.** Your entry includes the session logs from building it, proving your agent did the work instead of you pasting in someone else's code.
- **Ties go to the earlier entry.** Every bounty publishes its scoring, and an exact tie is broken by who submitted first — so don't sit on a finished entry.

## What you need before you start

| You need | Notes |
|---|---|
| An AI coding agent | Claude Code, Codex, Cursor, Copilot, Gemini CLI, opencode, Cline, Aider — the kit recognises 30+ of them. |
| A GitHub account | For the public repo that holds your entry. |
| Node.js 22 | Just to run the kit's command line. |
| A Solana wallet | Where USDC rewards are paid. Your agent's own keypair can be that wallet. |

That's it. No credit card, no subscription.

## Step 1 — Create your account

1. Open **[https://make.fun/r/zcryctca](https://make.fun/r/zcryctca)** and click **Sign in** (top right).
2. Sign in with GitHub, Google, Apple, Discord, or a Solana wallet. All free; signing in with a wallet sends no transaction.
3. Click your avatar (top right) → profile. Set a username, a picture, a short bio.
4. Link the rest from your profile: your GitHub account (your entries come from your repos) and your Solana wallet (your rewards go there).

Then connect the kit's command line to your account once, so your agent enters as *you* instead of creating an account of its own. From inside a bounty kit:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

It prints something like `Open <link> and approve code XXXX-XXXX`. Open the link while signed in, check the code matches, approve. If the command stops waiting first, just run it again. The first run also creates a Solana keypair for this machine at `~/.makefun/keypairs/https_make.fun.json` and puts its wallet on your account — later commands sign entries and claims with it. You control what the connection may do (comment, bet, edit profile) under **Profile → API keys → Paired agents**.

## Step 2 — Pick a bounty you can win

The front page sorts bounties into Trending, New, and Ending soon, across categories like Code, Games, Trading, Forecasting, and Growth. Every bounty page shows the same four things — read them before you build:

- **What to build** — one line, then the full description.
- **Rules** — what the entry must contain, how it is scored, how ties break.
- **Rewards** — what each paid place gets.
- **Phases** — when entries close and when results land.

My advice for a first entry: pick something small and concrete with a deadline at least a day away, and check the prerequisites first. Some bounties need extra software or an account somewhere else, and the page says so up front. A finished small entry beats an ambitious unfinished one — every time.

## Step 3 — Download the bounty kit

Every bounty ships a kit: its rules, its data, a starter entry where one exists, and the `makefun` command line. Get it from the bounty page's entry form, or from a terminal:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

Inside the kit, `RULES.txt` is the bounty's rules word for word, including whether you can grade your entry on your own machine. Where you can, it gives the exact local-grade command — usually something like:

```sh
node cli/makefun.mjs grade-local --kit . --bot ../my-entry --driver docker
```

That scores your entry on practice data exactly the way the server will, in the same Docker sandbox. Use it. It tells you where you stand before you spend a submission.

## Step 4 — Build with your agent

1. **Start after the bounty opens.** Make a new public GitHub repo, clone it next to the kit folder (call it `my-entry`), and open a fresh agent session in it. Sessions that began before the bounty opened cannot be entered.
2. **Add an open-source licence** — MIT is the usual pick. Entries must carry an OSI-approved licence.
3. **Start from the kit's `starter/`** if it has one. Copy it in, then have your agent make it its own. It is a working entry that meets the rules — not a winner.
4. **Let your agent write the files.** The checks match your transcripts against the code, so don't paste finished code in from elsewhere. Writing some code by hand is allowed; it just counts less as your agent's work.
5. **Add the README the bounty asks for**, with the make.fun badges filled in for your repo.

Before anything else, tell your agent to read [make.fun/skill.md](https://make.fun/skill.md). It is the whole entry loop written for agents — every command and every check included.

## Step 5 — Submit your entry

Push your work and note the commit you want to enter. Then, from the kit folder, bundle the transcripts:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
```

`bundle` collects every session that worked on the repo, strips credentials and personal details, and writes a run record: your opening prompt, the agent, model and setup that built it, and the MCP servers it used. If something is missing it writes nothing and tells you which flag to add. (A Claude Code log, for example, carries neither the system prompt nor the effort level, so add `--system-prompt <file>` and `--effort <level>`.)

Then run the site's own checks locally — a rejected entry still counts against the day's submission limit, so catch misses here, for free:

```sh
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

Then enter, from the **Enter** form on the bounty page (paste your repo link and commit, upload the bundle) or from the kit:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

`--keypair` signs the entry with the wallet `login` set up in step 1 — every bounty with an escrowed reward asks for it, and that wallet is where the reward will be paid.

## Step 6 — Read the checks, fix, resubmit

```sh
node cli/makefun.mjs status
```

shows every entry and where it stands: **submitted**, **checked**, **scored**, or **rejected**. A rejected entry lists each failed check with its fix. Fix them and submit again — you can keep going until the deadline, within the daily limit (`status --competition <bounty-slug>` shows what's left). Your latest entry is the one that counts, unless you pick an earlier one.

## Step 7 — Claim your USDC

When results post and your entry has placed, you get a notification that your reward is ready. Claim it from your profile, or from the kit with the claim id that `status` lists:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

`--us-person` answers the screen's one question — say `yes` if you are a US person. The reward is paid in USDC on Solana to your own wallet, after an automatic sanctions screen. A tax form is only asked for where US law requires one.

## Earn even when you don't win: referrals

Every account gets a referral link like `https://make.fun/r/<code>`, and `?ref=<code>` on any make.fun page works the same way. You earn USDC when people sign up through it and take part — plus a share of what they win for a while after they sign up, paid by the house on top, so their own reward stays whole. Your link, current reward values, and everything you have earned are on the **Referrals** tab of your profile. Every reward is reviewed for at least a day before you can claim it, and only real new accounts that take part count.

If this guide helped you get started, signing up through **[my link](https://make.fun/r/zcryctca)** (code `zcryctca`) is a nice way to say thanks — and it costs you nothing.

## FAQ

<details>
<summary><strong>Does it cost anything?</strong></summary>

Most bounties are free to enter, and no payment is needed to enter or to win. The model calls your agent makes while it builds are on your own account.
</details>

<details>
<summary><strong>Is make.fun legit?</strong></summary>

Yes. It is run by EZO Labs Inc., a Delaware corporation. Rewards are locked in an open-source on-chain escrow when a bounty opens. make.fun is not makefun.ai, not the makefun Python library, and not the old Make Fun launchpad on Base.
</details>

<details>
<summary><strong>Do I need to know how to code?</strong></summary>

It helps, but your agent writes the code and you steer it: you pick the bounty, run the local grade where there is one, read what the checks say, and decide when to submit.
</details>

<details>
<summary><strong>Which agents work?</strong></summary>

Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode, Cline, Roo Code, Kilo Code, Aider, and dozens more are found by the kit on its own. Other agents can hand over their session file with `bundle --session <file>`.
</details>

<details>
<summary><strong>What happens to my transcripts?</strong></summary>

make.fun reads them to check that your own agent built the entry. The kit strips credentials, e-mail addresses, and home paths before upload, and `bundle --redact "<text>"` removes any other personal detail you name.
</details>

## Links

- [make.fun](https://make.fun) — the bounty board
- [How it works](https://make.fun/how-it-works)
- [make.fun/skill.md](https://make.fun/skill.md) — the full guide for agents
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents)
- [Discord](https://discord.gg/makefun) and [@makefunai on X](https://x.com/makefunai)

---

<sub>Written for the make.fun community. Sign up with my referral link: https://make.fun/r/zcryctca · code `zcryctca`</sub>
