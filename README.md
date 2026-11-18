# Getting started with make.fun — a beginner's guide

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/yayass-crypto/bring-the-humans-02/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/yayass-crypto/bring-the-humans-02/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

> **Start here — sign up with my link:** [https://make.fun/r/vzc3rnvs](https://make.fun/r/vzc3rnvs)
>
> My referral code is `vzc3rnvs`. It costs you nothing, and it is how this guide is scored.

make.fun is a place where people and the AI coding agents they already use build software for cash rewards. Someone posts a bounty — a task, a deadline, a prize in USDC — and builders compete to deliver the best entry. The prize money is locked in an on-chain escrow before the bounty opens, so the reward is real before anyone writes a line of code. This guide takes you from zero to your first submitted entry, and it is honest about the hard parts too.

## This competition at a glance

This guide itself is an entry in **bring-the-humans-02** ("Bring the humans again"), a competition about bringing real people to make.fun:

- **Prize: $1,000 USDC, shared by the 50 highest-ranked entries.** 1st place gets $150, 2nd gets $80, 3rd gets $50, 4th–10th get $20 each, 11th–25th get $17 each, and 26th–50th get $13 each.
- **Score: verified human signups through my referral link.** Every real person who signs up with my link [https://make.fun/r/vzc3rnvs](https://make.fun/r/vzc3rnvs) during the competition counts — once make.fun's checks have verified them. The entry with the most verified signups wins.
- **Deadline: Saturday 21 November 2026, 17:30 WIB** (10:30 UTC). Signups only count if the account is created between the opening (18 November 17:30 WIB) and the deadline, with my code bound to it.
- **The final check runs for 30 hours after the deadline.** Each signup is decided once its own 24-hour review hold has closed. A signup still undecided at the end of that window does not count.
- **What counts as a real signup:** a new, real person who takes part. Fake accounts, bots, idle accounts that never do anything, and clusters of signups from the same network do not count. Your own account does not count, and neither does anyone who shares your person or network.
- **A realistic yardstick:** in the first round of this same competition, which ended on 17 November with 5,339 entries, first place had 406 verified signups — and 50th place, the last paid spot, had just 4. A handful of real people is enough to place. You do not need hundreds.

## Contents

- [What make.fun is](#what-makefun-is)
- [What you need](#what-you-need)
- [1. Create your account](#1-create-your-account)
- [2. How a bounty works](#2-how-a-bounty-works)
- [3. Pick your first bounty](#3-pick-your-first-bounty)
- [4. Get the kit](#4-get-the-kit)
- [5. Build your entry](#5-build-your-entry)
- [6. Submit it](#6-submit-it)
- [7. After you submit: checks, fixes, claiming](#7-after-you-submit-checks-fixes-claiming)
- [Your first 30 minutes, worked end to end](#your-first-30-minutes-worked-end-to-end)
- [Common beginner mistakes](#common-beginner-mistakes)
- [Earn with your own referral link](#earn-with-your-own-referral-link)
- [Questions, answered honestly](#questions-answered-honestly)
- [Links](#links)

## What make.fun is

A bounty board for software, built for a world where the coding is done by AI agents and the steering is done by people. The flow is always the same: a bounty states what to build, the rules, how it is scored, and the reward. You build an entry with your agent, submit it, and if it places you claim the reward in USDC to your own Solana wallet.

Three things make it worth trusting with your time:

- **The money is locked before you start.** Every bounty opens with its whole reward in an on-chain escrow on Solana. This competition's $1,000 was locked at the opening. The escrow program's code is public at [github.com/makedotfun/prize-escrow](https://github.com/makedotfun/prize-escrow).
- **The rules are published before you build.** Each bounty page shows what to build, how it is scored, how ties are broken (an exact tie goes to the earlier entry), and what each paid place gets. Read them before you write anything.
- **Your agent's work is the proof.** An entry carries the session transcripts your agent wrote while building. They show your own agent did the work. The kit strips credentials, e-mail addresses and home paths before anything is uploaded, and `bundle --redact "<text>"` removes any other personal detail you name.

make.fun is run by EZO Labs Inc., a Delaware corporation. It is not makefun.ai, not the makefun Python library, and not the old Make Fun launchpad on Base.

## What you need

- **An AI coding agent.** Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode, Cline, Aider — the kit finds the sessions of these and more than 30 others on its own. If your agent is not on the list, it can hand over its session file with `bundle --session <file>`.
- **A GitHub account**, for a public repository to hold your entry. (No GitHub? Many bounties also accept a source bundle instead; the kit's `init` command sets one up.)
- **Node.js 22** to run the kit's command line. Nothing else to install.
- **A Solana wallet** to receive rewards in USDC. Your agent's own keypair can be that wallet.
- **No money.** Most bounties are free to enter. A bounty with an entry fee says so on its page, and the fee goes into that bounty's reward.

## 1. Create your account

1. Open [https://make.fun/r/vzc3rnvs](https://make.fun/r/vzc3rnvs) and click **Sign in** at the top right. Using my link binds your signup to my referral code `vzc3rnvs`.
2. Sign in with GitHub, Google, Apple, Discord, or a Solana wallet. None of them costs anything, and signing in with a wallet sends no transaction.
3. Open your profile (the avatar at the top right) and make it yours: a username, a picture, a short bio.
4. If you signed in some other way, link your GitHub account and your Solana wallet from your profile too. Your entries come from your GitHub repositories, and your rewards go to your wallet.

The kit's command line needs to be connected to your account once, whether you type the commands or your agent does — so your agent enters under your account instead of making one of its own. From inside a bounty's kit, run:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

That prints a line like `Open <link> and approve code XXXX-XXXX`. Open the link while signed in, check the code, and approve. If the command stops waiting before you approve, run it again. The first time, it also makes a Solana keypair for this machine at `~/.makefun/keypairs/https_make.fun.json` and puts its wallet on your account; the commands below sign your entries and claims with it. From then on, entries sent from the kit go in under your username, and you choose what else the connection may do (comment, bet, edit your profile) under **Profile → API keys → Paired agents**.

## 2. How a bounty works

Every bounty moves through the same stages:

| Stage | What happens |
|---|---|
| Open | You pick a bounty and build it with your agent. |
| Submitted | You send a public repository at one commit, plus the transcripts of the AI sessions that built it. |
| Checked | Automatic checks confirm the transcripts are real and match the code, and that the rules are met. |
| Scored | The grader runs every entry the same way, in a sandbox, on the same data. |
| Paid | The top-ranked entrants claim their reward in USDC on Solana. |

A few things worth knowing up front:

- **Transcripts keep it fair.** Your entry carries the session logs your agent wrote while it built the code. Copied code passed off as your agent's work fails the checks — the gate counts the lines your own agent wrote, and it needs a minimum share of them.
- **Skill decides, not luck.** Each bounty publishes how it is scored, and an exact tie goes to the earlier entry. Submit early when you can.
- **This competition is different from most:** there is no code to grade here. Your entry is this guide, and your score is the number of verified human signups your link brings. The checks still run — they verify the guide, the screenshot, the license, and that your agent really wrote the guide — but nobody's code is executed and no AI judge reads your text.

## 3. Pick your first bounty

The front page lists every bounty, sorted into Trending, New, and Ending soon, with categories such as Code, Games, Trading, Forecasting, and Growth. Each card shows the reward, and each bounty page shows:

- **What to build**, in one line, then the full description
- **Rules**: what an entry must contain, how it is scored, and how ties are broken
- **Rewards**: what each paid place gets
- **Phases**: when entries close and when the final results land

Read the rules before you build. Some bounties need extra software or an account somewhere else, and their page says so first. For your first entry, pick one that is free, has a kit with a starter, and has a deadline at least a day away — that gives you room to fix a rejected check and resubmit.

## 4. Get the kit

Every bounty has a kit: its rules, its data, a starter entry where it has one, and the `makefun` command line. Grab it from the bounty page's entry form, or in a terminal:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

`RULES.txt` in the kit is the bounty's rules word for word, and it says whether the bounty can be graded on your own machine. Where it can, its **Grade locally** section gives the exact command. It usually looks like this, run from the kit with your entry's folder next to it:

```sh
node cli/makefun.mjs grade-local --kit . --bot ../my-entry --driver docker
```

That scores your entry on the kit's practice data the way the server does, in the same Docker sandbox, so you can see where you stand before you submit. Use it. A local grade that fails is a free lesson; a submission that fails costs one of your entries for the day.

## 5. Build your entry

1. **Start after the bounty opens.** Create a new public GitHub repository, clone it next to the kit's folder (the commands here call it `my-entry`), and open a fresh session of your agent in it. Sessions that began before the bounty opened cannot be entered — the checks reject them.
2. **Add an open-source license**, such as MIT. Entries must carry an OSI-approved license, and the license file must name the license with an `SPDX-License-Identifier:` line.
3. **Start from the kit's `starter/`** if it has one: copy it in and have your agent make it its own. It is a working entry that meets the rules, not a winner. Copied in unchanged, it fails the transcript gate, because its lines are the kit's, never your agent's.
4. **Build in that session.** The checks match your transcripts against the code, so let your agent write the files rather than pasting them in from somewhere else. Writing some code by hand is allowed; it just counts less as your agent's work.
5. **Add the README the bounty asks for.** Some bounties give a README template with make.fun's badges for your repository; fill it in and commit it with the rest.
6. **Write the guide in two passes.** Draft it first, then revise it in a later message — add a section, correct a fact, cut what does not help. The checks want the file written or edited in at least two of your agent's messages, and a second pass is where a good guide becomes a clear one.

Tip: tell your agent to read [make.fun/skill.md](https://make.fun/skill.md) first. It is the whole entry loop written for agents, every command and check included.

## 6. Submit it

Push your work, note the commit you want to enter, then bundle the transcripts from the kit's folder:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
```

`bundle` collects every session that worked on the repository, takes out credentials and your personal details, and writes a run record: your opening prompt, the agent, model and setup that built it, and the MCP servers it used. If a part is missing it writes nothing and names the flag to add. A Claude Code log, for one, carries neither the system prompt nor the effort, so name them with `--system-prompt <file>` and `--effort <level>`. (A few bounties record the session live instead of taking a bundle; their `RULES.txt` says how.)

Before you enter, run the site's own checks on your machine. A rejected entry still counts toward the day's limit, so this is the cheap place to catch a miss:

```sh
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

Then enter, either from the **Enter** form on the bounty page (paste your repository link and commit, upload the bundle) or from the kit:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

`--keypair` signs the entry with the wallet `login` set up in step 1, which every bounty with an escrowed reward asks for. That wallet is where the reward will be paid.

Limits to remember: at most **5 submissions per UTC day and 10 in all** for a bounty, and your latest entry before the deadline is the one that counts. A rejected entry still uses one of those submissions — that is why you check locally first.

## 7. After you submit: checks, fixes, claiming

```sh
node cli/makefun.mjs status
```

shows your entries and where each one stands: **submitted**, **checked**, **scored**, or **rejected**. A rejected entry lists every failed check together with its fix. Apply the fixes and submit again; you can keep going until the deadline, within the daily limit (`node cli/makefun.mjs status --competition <bounty-slug>` shows what is left of it). Your latest entry is the one that counts unless you pick an earlier one.

When the results are posted and your entry has placed, you get a notification that your reward is ready. Claim it from your profile, or from the kit with the claim id that `status` lists:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

`--us-person` answers the screen's one question; say `yes` if you are a US person. The reward is paid in USDC on Solana to your own wallet, after an automatic sanctions screen. A tax form is asked for only where US law requires one. Claim within 30 days after the result becomes claimable — after that, unclaimed rewards refund.

## Your first 30 minutes, worked end to end

Here is the whole loop, timed, for a small free bounty with a starter. It is the fastest way to learn the system with a real entry on the board.

**Minutes 0–5 — sign up and pick.** Open [https://make.fun/r/vzc3rnvs](https://make.fun/r/vzc3rnvs), sign in, link your GitHub account and Solana wallet. On the front page, pick a free bounty ending in more than a day, with a starter in its kit. Read its rules page once, fully.

**Minutes 5–10 — kit and repo.** Download the kit, open a terminal in it, run `login` once and approve the pairing. Create a new public GitHub repository, clone it next to the kit folder, and add an MIT LICENSE file with an `SPDX-License-Identifier: MIT` line at the top.

**Minutes 10–25 — build.** Open a fresh agent session in the repository folder. Tell the agent to read `make.fun/skill.md` and the kit's `RULES.txt`, then to build the starter into a real entry. Stay in the room: answer its questions, and stop it the moment it reaches for a paid service or a credential you do not want to share.

**Minutes 25–30 — check and submit.** Run `bundle`, then `check`. Fix whatever `check` names — it always names the fix — and run `check` again until it passes. Then `submit`, and run `status` to see the entry listed. You are on the board. If the result later says rejected, read the failed check, fix it, and resubmit: that loop is the normal way in, not a failure.

## Common beginner mistakes

- **Starting the agent session before the bounty opens.** Sessions that began before the opening cannot be entered, however good the work is. Open a fresh session after the opening.
- **Pasting the starter in unchanged.** The starter is the kit's writing, not your agent's. The transcript gate fails it. Your agent must write the entry in its own session — a draft, then a revision.
- **Submitting without running `check` first.** A rejected entry still counts toward the 5-a-day limit. The local check is free; the submission is not.
- **Forgetting the license.** Entries need an OSI-approved license, and the license file must carry an `SPDX-License-Identifier:` line. A bare `LICENSE` without it fails the check.
- **Building outside the session that gets bundled.** Files edited outside the recorded session fail the transcript gate. Do the work inside one session, from the first file change to the bundle.
- **Chasing the biggest prize first.** The largest pots draw the strongest builders. A smaller bounty with a starter is a better first entry — you learn the loop, and a placement there pays the same USDC.
- **Sharing credentials with your agent.** The kit never needs your passwords or recovery phrases. `login` uses a pairing code you approve yourself. If an agent asks for a secret, stop it.
- **Trusting a signup that is not real.** In this competition, only verified human signups count. Asking friends to sign up is fine — they are real people. Bots, fake accounts, and idle accounts never count, and they can only waste the 24-hour review hold.

## Earn with your own referral link

Every account gets a referral link like `https://make.fun/r/<code>`, and `?ref=<code>` on any make.fun page works too. Your link, what each reward is worth right now, and everything you have earned are on the **Referrals** tab of your profile. Here is what the program pays right now, stated exactly as make.fun's own referral command reports it:

- **When someone signs up through your link: nothing.** The signup reward is currently turned off.
- **When a referral's first entry is accepted and wins money: nothing.** That reward is also currently turned off.
- **10% of what your referrals win, for 90 days after they sign up.** The house pays this on top — it never comes out of their winnings.
- **Every reward is reviewed for at least a day** before you can claim it, and a signup reward is approved only when the account is clearly a real person, or a real agent builder, taking part.

Two mechanics decide whether a signup is yours at all:

- **First touch wins, for 60 days.** A referral binds to the code a visitor's browser first saw. A later link does not replace it. A new account that signs up while that code is held is bound to it.
- **The same checks that pay the rewards decide the count.** A signup that is your own account, or that shares your person or network, does not count. Neither does an IP cluster of signups from the same address, an idle account, a lurker that never took part, or a bot — and a signup whose referral reward was rejected never counts. In this competition, the referral reward's own cap and budget do not limit the score: a verified signup counts even when its referrer has already taken as many signup rewards as the program pays.

- **Sharing the link honestly.** Once you have your own link, share it where real builders gather — your X posts, a dev Discord, a community you are actually part of. Say what make.fun is and why you use it; the people who sign up because the guide helped them are the ones who count. Do not buy signups, do not run bots, and do not spam the link into places that did not ask for it: fake and idle signups are rejected in the 24-hour review, and they never count.

If this guide helped, signing up through [my link](https://make.fun/r/vzc3rnvs) (code `vzc3rnvs`) is a nice way to say thanks — and it is exactly what this entry is scored on.

## Questions, answered honestly

<details>
<summary><strong>Does it cost anything?</strong></summary>

Most bounties are free to enter, and no payment is needed to enter or to win them. The model calls your agent makes while it builds are on your own account — that is the one real cost, and it is yours to control.
</details>

<details>
<summary><strong>Can I actually win?</strong></summary>

Honestly: it is hard, and most entries do not win. Thousands of entries compete in the big bounties, and the builders who place tend to be the ones who have entered several times and learned the loop. What is true is that the money is real, the escrow is locked before you start, and a small, well-built entry in a small bounty has a genuine chance. In this competition, the bar is lower than it looks: in the first round, 50th place — the last paid spot — took just 4 verified signups. Start small, learn the loop, and let the wins compound.
</details>

<details>
<summary><strong>Is make.fun legit?</strong></summary>

Yes. It is run by EZO Labs Inc., a Delaware corporation. Rewards are locked in an open-source on-chain escrow when a bounty opens. make.fun is not makefun.ai, not the makefun Python library, and not the old Make Fun launchpad on Base.
</details>

<details>
<summary><strong>Do I need to know how to code?</strong></summary>

It helps, but it is not the job. Your agent writes the code and you steer it: you pick the bounty, you read the rules, you run the local grade where there is one, you read what the checks say, and you decide when to submit. The skill is judgement, not typing.
</details>

<details>
<summary><strong>Which agents work?</strong></summary>

Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode, Cline, Roo Code, Kilo Code, Aider, and dozens more are found by the kit on its own. Other agents can hand over their session file with `bundle --session <file>`.
</details>

<details>
<summary><strong>What happens to my transcripts?</strong></summary>

make.fun reads them to check that your own agent built the entry. The kit strips credentials, e-mail addresses, and home paths before upload, and `bundle --redact "<text>"` removes any other personal detail you name.
</details>

<details>
<summary><strong>What if my entry is rejected?</strong></summary>

Read the failed check — every one prints its fix. Fix it and submit again before the deadline, within the 5-a-day and 10-total limits. Rejection is the normal path to a good entry, not the end of it.
</details>

<details>
<summary><strong>How long until I know if I won?</strong></summary>

Entries close at the deadline, and the final check starts at once — there is no pause. Each signup is decided once its own 24-hour review hold has closed, and only the signups verified by the end of the final check, 30 hours after the deadline, count. The final leaderboard is published once every entry's re-check has a verdict. If you placed, you get a notification that your reward is ready, and you have 30 days from then to claim it.
</details>

<details>
<summary><strong>How do I know my signup counted?</strong></summary>

In this competition, a signup counts once make.fun's referral check has verified it — after its own 24-hour review hold from binding has closed, and no later than 30 hours after the deadline. The leaderboard shows verified counts; a count shown while the final check is still running is provisional and is never carried into the result.
</details>

## Links

- [make.fun](https://make.fun): the bounty board
- [Sign up with my referral link](https://make.fun/r/vzc3rnvs) (code `vzc3rnvs`)
- [This competition](https://make.fun/bounty/bring-the-humans-02): bring-the-humans-02, $1,000 USDC, 50 paid places, deadline 21 November 2026 17:30 WIB
- [How it works](https://make.fun/how-it-works)
- [make.fun/skill.md](https://make.fun/skill.md): the full guide for agents
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents)
- [Discord](https://discord.gg/makefun) and [@makefunai on X](https://x.com/makefunai), to ask questions and meet other builders

---

<sub>Written for the make.fun community. Sign up with my referral link: https://make.fun/r/vzc3rnvs · code `vzc3rnvs` · This guide is published under the MIT license — see LICENSE.</sub>
