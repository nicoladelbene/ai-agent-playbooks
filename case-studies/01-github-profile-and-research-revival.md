# Case study: rebuilding a GitHub profile and reviving a 2020 research project with Claude Code

**In short:** I gave my AI coding agent (Claude Code) a vague request: "update my GitHub profile from scratch." It turned into a structured, interview-driven session. In one afternoon the session produced:

- a rebuilt GitHub profile (bio, links, profile README), set up through the GitHub CLI,
- my 2020 MSc thesis software, recovered from old laptop backups into a private repository,
- the thesis benchmark results **reproduced exactly**, using free software (GNU Octave instead of MATLAB),
- a literature review that checks whether the research is still novel six years later,
- a plan to publish, with rules for co-authorship and data protection.

I didn't write a line of code. I answered questions.

---

## 1. Start with an interview, not a to-do list

I didn't describe what I wanted in detail. I used the **Grilling** skill (from [Matt Pocock's skills](https://github.com/mattpocock/skills)). It makes the agent interview you in **rounds**. Each question comes with a recommended answer, and you can reply "yes" to accept it.

The questions came in a sensible order, because each round only asks what can be decided given the answers so far:

| Round | What was decided |
|---|---|
| 1 | Username, audience (recruiters + portfolio), language, how changes get applied (CLI vs copy-paste), how much to reset |
| 2–3 | Current role, location, links, bio wording (160-character limit), profile README draft |
| 4–6 | What to do with old research code: co-authors, open-source vs private, what language to port to, which data to use |
| 7–9 | What to do *while waiting* for collaborators, cloud data access, costs (CHF 0/month), a public repo |

**Why this works:** most of my answers were "yes" or one sentence long. The agent did the drafting; I only made the decisions. See the [Grilling guide](../guides/grilling-to-stress-test-a-plan.md).

## 2. Let the agent find facts; keep the decisions yourself

Several times the agent **looked things up instead of asking me**:

- It found my GitHub username through the CLI login after a public lookup by email failed (my email is private on GitHub).
- It found my 2020 thesis in the university repository, which confirmed the co-author, the dataset size and the results.
- It **searched my own laptop** and found ~70 MATLAB files from 2020, three older copies of them, a forgotten draft paper, and benchmark result files from a colleague.
- It read the 209-page thesis PDF, compared the two versions, and worked out that the later one was the final version with the personal acknowledgements removed.

What it *didn't* do was decide for me. It asked about authorship order, who to contact first, what goes public and the budget.

> **Lesson:** a good agent session is a division of labour. Facts are the agent's job, decisions are yours.

## 3. Automate the boring part with official tools

The profile update used the official GitHub CLI (`gh`):

```bash
gh api -X PATCH user -f name="…" -f bio="…" -f company="…" -f location="…"
gh api -X POST user/social_accounts -f 'account_urls[]=https://www.linkedin.com/in/…'
gh repo create <username> --public   # the special "profile README" repository
```

The agent showed me every piece of text **before** applying it. One thing can't be done through the API (pinning repositories, and one privacy setting), so it gave me exact click paths for those.

**Small gotcha worth knowing:** device login codes expire. My first login attempt timed out, so the agent started the login in the background and gave me the one-time code to enter in the browser.

## 4. Recovering old research: inventory first, then a private repository

Before uploading anything, the agent:

1. **compared the copies** (by hashing the files) to find the newest version of the code,
2. **downloaded iCloud placeholders** that only looked like they were on disk,
3. **scanned for data files**, because the research used hospital ICU recordings. Even de-identified data must never go into a repository,
4. read the copyright headers to list everyone who must agree before any public release,
5. noted third-party code that needs its licence checked.

Everything went into a **private** repository with a `.gitignore` that blocks waveform and data file types. It stays private until co-authors agree.

## 5. Reproduce before you improve

The most satisfying part. The original code needed MATLAB, which I no longer have. The agent:

1. installed **GNU Octave** (free) and the matching signal-processing package,
2. downloaded the public benchmark datasets (PhysioNet/CinC Challenge 2014, MIT-BIH Arrhythmia),
3. wrote two small **compatibility shims**, because two MATLAB functions behave differently in Octave,
4. ran the **unchanged 2020 code** and scored it the way the 2020 scripts did.

| Dataset | Thesis (2020, MATLAB) | Reproduced (2026, Octave) |
|---|---|---|
| Challenge 2014 training set | 99.91 | **99.91** |
| MIT-BIH Arrhythmia | 99.49 | **99.49** |
| Challenge 2014 augmented set | 89.46 | 89.44 |

It then compared the results **record by record** with the 2020 result files. It explained the tiny difference (14 very noisy recordings, consistent with numerical filtering differences) instead of hiding it.

> **Lesson:** "reproduce before you improve" gives you a solid baseline and reference outputs for any later rewrite (here, a Python port).

## 6. Guardrails for regulated data

The project uses a credentialed clinical database. Its licence **forbids sending the data to third-party AI services** unless they guarantee zero data retention. So we agreed a simple rule, written into the agent's memory:

> The agent writes SQL and Python; I run it under my own login; only **aggregate** results (counts, metrics, plots without patient rows) come back to the agent.

Public, open-access datasets are fine to process directly. The same pattern applies to client data in consulting. See the [data-rules template](../templates/data-rules-CLAUDE.md).

## 7. Cost discipline

I asked for **zero cloud spend**. The agent recorded that as a lasting preference. It plans to try the free BigQuery sandbox, keeps a local DuckDB fallback, and asks before enabling any billing.

---

## What I'd tell a colleague

- Start every non-trivial task with an **interview** (Grilling), not a prompt.
- Insist the agent **shows drafts before acting** on anything public.
- Put **data rules** in writing (in `CLAUDE.md` or the agent's memory) *before* the first file is opened.
- For anything old or scientific: **inventory → reproduce → only then improve.**
