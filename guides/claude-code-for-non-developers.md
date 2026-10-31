# Claude Code for non-developers

Claude Code is an AI agent that runs in your terminal (and in desktop and IDE apps). It can read and write files, run commands and use the web. It's useful well beyond coding: research, document work, data analysis, automating admin.

This guide covers what you need to be productive **and safe**.

## 1. Setup (about 10 minutes)

1. Install Claude Code following the [official docs](https://code.claude.com/docs/en/overview).
2. Open a terminal **in a dedicated folder** for your task (`mkdir ~/Projects/my-task && cd ~/Projects/my-task`), then run `claude`.
3. Useful extras:
   - **Voice input:** `/voice` lets you dictate long context instead of typing it.
   - **Skills:** packaged workflows the agent can follow. A good starter set is [Matt Pocock's skills](https://github.com/mattpocock/skills):
     ```bash
     claude plugin install mattpocock-skills@claude-plugins-official
     ```
   - **GitHub CLI** (`brew install gh`), if you work with GitHub.

## 2. The mental model

| Think of it as… | …which means |
|---|---|
| A capable new colleague with no context | Give background: who you are, the goal, the constraints |
| Someone who acts on your machine | Be deliberate about what it may read, run and publish |
| Someone who doesn't remember tomorrow unless told | Use **memory** and a `CLAUDE.md` file for lasting rules |

## 3. Permissions: decide how much autonomy to give

Claude Code asks before running commands or editing files, unless you allow it not to.

- **Default (ask each time):** best while learning.
- **Allow-lists:** pre-approve safe, read-only commands so you get fewer prompts.
- **"Bypass" modes:** only in a throwaway folder or a sandbox, never in a folder containing confidential material.

> Rule of thumb: the more sensitive the folder, the less autonomy.

## 4. Make it ask you questions

The fastest way to get a good result is to make the agent **interview you** before it does anything. Type `/grilling` (or `/grill-me`) followed by your goal. See [the Grilling guide](grilling-to-stress-test-a-plan.md).

## 5. Memory and `CLAUDE.md`

- **`CLAUDE.md`** in a folder holds instructions the agent reads every time it works there: conventions, do's and don'ts.
- **Memory** holds facts about you and your preferences that carry across sessions, such as "zero cloud spend" or "never read patient data". Ask it to "remember that…".

## 6. Safety rules that matter most

These are the rules I follow and teach:

1. **Never put client, personal or regulated data in the agent's context** unless your organisation has approved that exact setup. That includes files it reads, query results and pasted text.
2. **Use the code-only pattern** for sensitive data: the agent writes the code, *you* run it, and only aggregate results go back. Template: [`data-rules-CLAUDE.md`](../templates/data-rules-CLAUDE.md).
3. **Check the data licence.** Some research datasets explicitly forbid sending data to online AI services.
4. **Review before anything is published:** GitHub repos, emails, posts. Ask the agent to show you the exact text first.
5. **Private by default.** Create repositories as private and make them public deliberately.
6. **Keep secrets out:** API keys go in environment variables or a password manager, never in files the agent might commit.

## 7. Good first tasks

- Reorganise and summarise a folder of old documents.
- Draft a profile or bio and apply it through an official CLI ([case study](../case-studies/01-github-profile-and-research-revival.md)).
- Turn a messy spreadsheet into a clean analysis notebook, **using non-sensitive data**.
- Research a topic and get a sourced Markdown summary.

## 8. Signs a session is going well

- It **asks before deciding** things that are yours to decide.
- It **looks up facts** instead of asking you for them.
- It **shows you drafts** before public actions.
- It **reports honestly**, including small discrepancies and failures.
