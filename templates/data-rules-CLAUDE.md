# Data-handling rules for AI agents (CLAUDE.md template)

Copy the block below into a `CLAUDE.md` file at the root of any folder where an AI agent works near sensitive data, then adapt the paths and categories.

```markdown
## Data rules (non-negotiable)

Sensitive data in this project: <client data | personal data | credentialed research data (e.g. MIMIC)>.
It lives in: <paths / databases>. These are NEVER to be read, printed, summarised or uploaded by the agent.

- Code-only pattern: the agent writes code/SQL; the human runs it under their own login.
- Only aggregate outputs may be shared back with the agent: counts, metrics, model scores,
  plots WITHOUT individual records. Suppress small cells (n < 10).
- Never `cat`, `head`, open or query sensitive files/tables directly, even "just to check the format".
  Ask the human for the schema instead.
- Never copy sensitive data into this repository. `.gitignore` must block data file types.
- Open/public datasets (list them: <…>) may be processed directly.
- Nothing is published (repos made public, posts, emails) without explicit human review of the exact content.
- If unsure whether something is sensitive, stop and ask.
```

## Why

- Many data licences (e.g. PhysioNet's credentialed data use agreement) **restrict sending data to third-party AI services**, and a provider's retention promise may not be enough. Check the current terms.
- Client and personal data are usually covered by contracts and privacy law (e.g. GDPR / Swiss FADP).
- An agent that "just looks at the first rows" has already sent those rows to a model.

## Matching `.gitignore` starter

```gitignore
data/
*.csv
*.parquet
*.xlsx
*.dat
*.hea
*.atr
*.mat
.env
```
