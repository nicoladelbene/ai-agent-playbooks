# Stress-test any plan with the Grilling skill

**Grilling** is an interview technique for AI agents, packaged as a skill in [Matt Pocock's skills](https://github.com/mattpocock/skills) (`/grilling`, `/grill-me`, `/grill-with-docs`). Instead of you writing a perfect brief, the agent **asks you questions in rounds** until you share an understanding of the plan. Only then does it act.

## How it works

1. The agent maps your plan as a **decision tree**: every decision branches into the decisions that depend on it.
2. Each **round** asks only the questions that *can* be answered now (the "frontier"). It doesn't ask about details that depend on answers it doesn't have yet.
3. Every question comes with a **recommended answer**, phrased so that replying "yes" accepts it.
4. The agent **looks up facts itself** (files, web, tools). It only asks you about **decisions**.
5. It finishes when the tree is fully explored and you confirm the shared understanding.

A round looks like this:

> ❓ **Q2** - **Audience**: Who is the profile for: (a) recruiters, (b) clients, (c) developers, (d) personal portfolio?
>
> ➡️ Mostly (a), plus some (d).

## When to use it

- Anything with **several dependent decisions**: a profile refresh, a migration, a research plan, a client deliverable outline.
- When you **don't know what you don't know**.
- Before any **public or hard-to-reverse** action.

Skip it for one-step tasks ("rename these files").

## Tips from real use

- **Answer briefly.** "Agree with everything" is a valid answer, because the recommendations do the work.
- **Push back where it matters.** In my case I corrected who counted as a co-author, my budget (CHF 0) and how I'd contact people (WhatsApp, not email). Each correction reshaped the plan.
- **Give raw facts, not polished text.** Write your background as a stream of consciousness and let the agent draft from it.
- **Expect it to catch inconsistencies.** It noticed when something I said didn't match what was in my files, and asked me to confirm instead of guessing.
- **Keep grilling throughout.** Each new phase (what to do while waiting, cloud migration, a public repo) got its own short round.

## Copy-paste starter

```text
/grilling I want to <goal>. Context: <who I am, constraints, deadline, budget>.
Things that must not happen: <e.g. nothing public without my review; no client data in context>.
Ask me questions in rounds with your recommended answer; look up facts yourself.
```

## Why it works

Most failed AI sessions fail because of a **communication gap**: the agent guesses at intent. Grilling turns that around. The agent does the structured thinking and drafting, and you make a small number of high-value decisions.
