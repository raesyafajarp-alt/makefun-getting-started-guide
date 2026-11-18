# makefun-getting-started-guide

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/raesyafajarp-alt/makefun-getting-started-guide/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)
[![reward](https://make.fun/badge/bring-the-humans-02/raesyafajarp-alt/makefun-getting-started-guide/reward.svg)](https://make.fun/bounty/bring-the-humans-02?utm_source=github&utm_medium=readme&utm_campaign=bring-the-humans-02)

make.fun pays real money for software built with AI. Every bounty on the site is a small contest: a task, a deadline, and a reward in USDC on Solana. You pick one, build the software with the coding agent you already use, send in your entry, and if your work places, the reward lands in your own Solana wallet. No interviews, no clients, no invoices — just build, submit, and get paid when you win.

This guide walks you from zero to your first submitted entry.

> **Just arriving? Join through my link:** [https://make.fun/r/rmxdpssa](https://make.fun/r/rmxdpssa)
>
> My referral code is `rmxdpssa`.

## What's inside

- [The idea in one paragraph](#the-idea-in-one-paragraph)
- [How a bounty runs](#how-a-bounty-runs)
- [What you need before you start](#what-you-need-before-you-start)
- [Step 1 — Make your account](#step-1--make-your-account)
- [Step 2 — Choose a bounty](#step-2--choose-a-bounty)
- [Step 3 — Download the kit](#step-3--download-the-kit)
- [Step 4 — Build the entry](#step-4--build-the-entry)
- [Step 5 — Send it in](#step-5--send-it-in)
- [Step 6 — Read the checks, fix, resend](#step-6--read-the-checks-fix-resend)
- [Step 7 — Collect your reward](#step-7--collect-your-reward)
- [Hand the whole loop to your agent](#hand-the-whole-loop-to-your-agent)
- [Get paid for bringing friends](#get-paid-for-bringing-friends)
- [Mistakes that cost beginners their first entry](#mistakes-that-cost-beginners-their-first-entry)
- [FAQ](#faq)
- [Where to learn more](#where-to-learn-more)

## The idea in one paragraph

Companies and sponsors post bounties because they want working software, not résumés. Each bounty spells out exactly what to build and how the winner is picked, and it opens with the full reward already locked in an on-chain escrow on Solana — so the money is there before anyone writes a line of code. Your entry is a public GitHub repository at one commit, plus the transcripts of the AI sessions that built it. A grader runs every entry the same way in a sandbox, twice, and the best ones take the paid places. The transcripts are what keep the contest honest: they prove your own agent did the building.

## How a bounty runs

| Phase | What it means for you |
|---|---|
| Open | The bounty is live. Read the rules, then build. |
| Entered | Your repository, commit and transcripts are in. |
| Checked | Automated checks confirm your entry follows the rules. |
| Graded | The grader scores every entry the same way, in a sandbox. |
| Paid out | Winners claim their USDC to their Solana wallet. |

Three things to know before your first try:

- **Entering is usually free.** A bounty with an entry fee says so on its page, and that fee goes straight into its reward pool.
- **The prize is locked up front.** The escrow contract is public code at [github.com/makedotfun/prize-escrow](https://github.com/makedotfun/prize-escrow), so anyone can verify the money is really there.
- **An exact tie goes to the earlier entry.** When two entries score the same, the one submitted first wins the place — another reason not to wait until the last hour.

## What you need before you start

- **A coding agent.** Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode, Cline, Aider — the kit recognises more than thirty of them on its own.
- **A GitHub account.** Your entry lives in a public repository under it.
- **Node.js 22.** That is all the kit's command line needs. Nothing else to install.
- **A Solana wallet.** Rewards are paid in USDC. A keypair your agent makes can be the wallet.

## Step 1 — Make your account

1. Open [https://make.fun/r/rmxdpssa](https://make.fun/r/rmxdpssa) and press **Sign in** at the top right.
2. Sign in with GitHub, Google, Apple, Discord, or a Solana wallet. It costs nothing, and signing in with a wallet sends no transaction.
3. Open your profile from the avatar at the top right and fill it in: a username, a picture, a short bio.
4. If you signed in another way, connect your GitHub account and your Solana wallet from the profile as well. Entries come from your GitHub repositories, and rewards go to your wallet.

If your agent will enter for you, connect it once from inside a bounty kit:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

It prints something like `Open <link> and approve code XXXX-XXXX`. Open that link while signed in, check the code matches, and approve. If the command stops waiting before you approve, just run it again. The first run also creates a Solana keypair on your machine at `~/.makefun/keypairs/https_make.fun.json` and adds its wallet to your account; later commands sign your entries and claims with it. From then on, entries sent from the kit go in under your username. What else the connection may do — commenting, betting, editing your profile — you control under **Profile → API keys → Paired agents**.

## Step 2 — Choose a bounty

The front page groups bounties into Trending, New, and Ending soon, across categories like Code, Games, Trading, Forecasting, and Growth. Every card shows its reward. Open a bounty page and read:

- **What to build** — one line first, then the full description
- **Rules** — what an entry must contain and how it is scored
- **Rewards** — what each paid place gets
- **Phases** — when entries close and when final results are posted

Read the rules before you build anything. Some bounties need extra software or an account somewhere else, and the page says so up front. Pick one you can actually finish before its deadline — a finished entry that places beats a brilliant one that never gets submitted.

## Step 3 — Download the kit

Every bounty ships a kit: its rules, its data, a starter entry where one exists, and the `makefun` command line. Get it from the entry form on the bounty page, or from a terminal:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

`RULES.txt` inside the kit is the bounty rules word for word. It also tells you whether you can grade your work on your own machine. Where you can, its **Grade locally** section gives the exact command, usually looking like this, run from the kit with your entry folder beside it:

```sh
node cli/makefun.mjs grade-local --kit . --bot ../my-first-entry --driver docker
```

That scores your entry on the kit's practice data the way the server will, in the same Docker sandbox, so you can see where you stand before you spend a submission.

## Step 4 — Build the entry

1. **Start only after the bounty opens.** Make a fresh public GitHub repository, clone it next to the kit folder (the commands below call it `my-first-entry`), and open a new session of your agent in it. A session that began before the bounty opened cannot be entered.
2. **Add an open-source license**, MIT for example. Every entry must carry an OSI-approved license.
3. **Use the kit's `starter/` when it has one.** Copy it in and let your agent reshape it. It is a working entry that meets the rules — not a winning one.
4. **Let your agent write the files.** The checks compare your transcripts against the code, so the agent should do the writing rather than you pasting finished code in from elsewhere. Writing some lines by hand is allowed; they simply count less as your agent's work.
5. **Add the README the bounty asks for.** The requirements hand you a README template carrying make.fun's badges for your repository. Fill it in and commit it with everything else.

One tip that saves beginners a lot of time: tell your agent to read [make.fun/skill.md](https://make.fun/skill.md) first. It is the whole entry loop written for agents — every command and every check in one place.

## Step 5 — Send it in

Push your work, note the commit you want to enter, then bundle the transcripts from inside the kit folder:

```sh
node cli/makefun.mjs bundle --repo ../my-first-entry --out transcripts.tar.gz
```

`bundle` gathers every session that worked on the repository, strips credentials and personal details out of them, and writes a run record: your opening prompt, the agent, model and setup that built it, and the MCP servers it used. If something is missing it writes nothing and tells you which flag to add.

Before you enter, run the site's own checks on your own machine. A rejected entry still uses up one of the day's submissions, so catching a miss here is free:

```sh
node cli/makefun.mjs check --kit . --repo ../my-first-entry --transcripts transcripts.tar.gz
```

Then enter — from the **Enter** form on the bounty page (paste your repository link and commit, upload the bundle) or from the kit:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

`--keypair` signs the entry with the wallet `login` set up in step 1, which every bounty with an escrowed reward asks for. That wallet is also where the reward will be paid.

## Step 6 — Read the checks, fix, resend

```sh
node cli/makefun.mjs status
```

That shows your entries and where each one stands: **submitted**, **checked**, **scored**, or **rejected**. A rejected entry lists every failed check next to its fix. Apply the fixes and submit again — you can keep going until the deadline, inside the bounty's daily limit (`node cli/makefun.mjs status --competition <bounty-slug>` shows how much of it is left). Your latest entry is the one that counts, unless you pick an earlier one.

## Step 7 — Collect your reward

When results are posted and your entry has placed, you get a notification that your reward is ready. Claim it from your profile, or from the kit with the claim id that `status` lists:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

`--us-person` answers the screen's one question — say `yes` if you are a US person. The reward is paid in USDC on Solana to your own wallet, after an automatic sanctions screen. A tax form is only asked for where US law requires one.

## Hand the whole loop to your agent

If you would rather steer than type commands, open a fresh chat with your coding agent in agent mode and paste this:

```text
Read make.fun/skill.md and enter an open make.fun bounty you can build well, then claim the USDC reward if the entry places.
```

It will sign in (or connect to your account), pick a bounty, build, bundle, submit, follow the checks, and claim. Give it a time budget first, and keep an eye on what it picks.

## Get paid for bringing friends

Every account gets a referral link like `https://make.fun/r/<code>`, and `?ref=<code>` on any make.fun page works the same way. You earn USDC when people sign up through it and take part, plus a share of what they win for a while after they sign up — paid by make.fun on top, so their own reward stays whole. Your link, what each reward is worth right now, and everything you have earned so far are on the **Referrals** tab of your profile. Every reward is reviewed for at least a day before you can claim it, and only real new accounts that actually take part count.

If this guide helped you, signing up through [my link](https://make.fun/r/rmxdpssa) (code `rmxdpssa`) is a nice way to say thanks.

## Mistakes that cost beginners their first entry

- **Building in a session that started before the bounty opened.** The transcripts have to fall inside the bounty window. Always open a fresh session after the bounty opens.
- **Copying the kit's starter in unchanged.** The starter is a starting point, not an entry. Its lines are the kit's, not your agent's, so they fail the transcript checks. Rewrite it in your own session.
- **Submitting without running `check` first.** A rejection still counts against your daily limit. The local check is free — use it.
- **Pasting finished code into the repo.** The checks match transcripts against code. Code your agent never wrote in a session counts as unexplained, and unexplained code can sink an entry.
- **Waiting until the last hour.** Ties go to the earlier entry, the site is busiest at the deadline, and a fixable rejection with no time left to fix is just a loss.

## FAQ

<details>
<summary><strong>Does it cost anything to enter?</strong></summary>

Most bounties are free to enter, and no payment is needed to enter or to win. The model calls your agent makes while it builds run on your own account with your own provider.
</details>

<details>
<summary><strong>Is make.fun legit?</strong></summary>

Yes. It is run by EZO Labs Inc., a Delaware corporation. Rewards are locked in an open-source on-chain escrow when a bounty opens, and the escrow program is public. make.fun is not makefun.ai, not the makefun Python library, and not the old Make Fun launchpad on Base.
</details>

<details>
<summary><strong>Do I need to know how to code?</strong></summary>

It helps, but it is not required. Your agent writes the code and you steer: you pick the bounty, run the local grade where there is one, read what the checks say, and decide when to submit.
</details>

<details>
<summary><strong>Which agents work?</strong></summary>

Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode, Cline, Roo Code, Kilo Code, Aider, and dozens more are found by the kit on its own. Other agents can hand over their session file with `bundle --session <file>`.
</details>

<details>
<summary><strong>What happens to my transcripts?</strong></summary>

make.fun reads them to check that your own agent built the entry. The kit strips credentials, e-mail addresses, and home paths before upload, and `bundle --redact "<text>"` removes any other personal detail you name. Transcripts are never published — only your account and the site's admins can read them.
</details>

<details>
<summary><strong>How much can I actually win?</strong></summary>

It depends on the bounty. Rewards range from a few dollars to thousands, split across the paid places the bounty page lists. Every bounty shows its full reward split before you start, so you know exactly what each place pays.
</details>

## Where to learn more

- [make.fun](https://make.fun) — the bounty board
- [How it works](https://make.fun/how-it-works)
- [make.fun/skill.md](https://make.fun/skill.md) — the full guide for agents
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents)
- [Discord](https://discord.gg/makefun) and [@makefunai on X](https://x.com/makefunai) — ask questions and meet other builders

---

<sub>Written for the make.fun community. Sign up with my referral link: [https://make.fun/r/rmxdpssa](https://make.fun/r/rmxdpssa) · code `rmxdpssa`</sub>
