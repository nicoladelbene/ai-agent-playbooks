# AI Agent Playbooks

Practical, tested playbooks for **non-developers** (consultants, analysts, researchers, managers) who want to use AI coding agents such as **Claude Code** and **Codex** for real work, not just demos.

Everything here comes from things I've actually done. Each playbook shows the process, the decisions and the guardrails, not only the prompt.

## Contents

| | Playbook | What you'll get |
|---|---|---|
| 📖 | [Case study: rebuilding a GitHub profile and reviving a 2020 research project](case-studies/01-github-profile-and-research-revival.md) | A full real session: an interview-driven plan, automated profile setup, recovering old code, and reproducing 2020 results exactly in free software |
| 🧭 | [Claude Code for non-developers](guides/claude-code-for-non-developers.md) | Setup, how to think about permissions, skills, memory, and the safety rules that matter most (client, personal and regulated data) |
| 🔥 | [Stress-test any plan with the Grilling skill](guides/grilling-to-stress-test-a-plan.md) | How interview-driven planning works, when to use it, and a copy-paste template |
| 🧩 | [Template: data-handling rules for your agent](templates/data-rules-CLAUDE.md) | A `CLAUDE.md` snippet that tells your agent what it must never read or send |

## Principles

1. **Decisions belong to the human, facts to the agent.** Let the agent look things up; never let it silently decide for you.
2. **Nothing sensitive goes in the context window.** If data is confidential, regulated or personal, design the workflow so the agent writes the code and you run it.
3. **Reproduce before you improve.** When reviving old work, first prove you get the same numbers.
4. **Small, real, verified** beats big and impressive.

## Licence

Text: [CC BY 4.0](LICENSE). Code and config snippets: [MIT](LICENSE-CODE). You can reuse and adapt anything here as long as you credit the source.

---

<sub>Personal project. Views are my own. Tools evolve quickly, so check commands against the official docs.</sub>
