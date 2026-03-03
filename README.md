# /deep-research

Research any topic. Get a sourced playbook back.

```
/deep-research Dario Amodei's vision for AI safety
```

This skill launches 3-5 parallel web search agents, each covering a different angle (official sources, practitioner blogs, community discussion), then synthesizes everything into a single markdown document where every claim has a source URL.

## Examples

```
/deep-research Harness Engineering for AI Agents
/deep-research Agent-Browser
/deep-research Dario Amodei
/deep-research React Server Components --file rsc.md
/deep-research --file existing-playbook.md
```

| Input | What happens |
|-------|-------------|
| Just a topic | Creates `<topic-slug>.md` in your current directory |
| Topic + `--file path.md` | Writes to the specified path |
| `--file existing.md` only | Updates the existing playbook with new findings |

## Install

```bash
npx skills add webcpu/deep-research-skill
```

Then type `/deep-research` in Claude Code. That's it.

Or copy manually:

```bash
mkdir -p ~/.claude/skills/deep-research
curl -o ~/.claude/skills/deep-research/SKILL.md \
  https://raw.githubusercontent.com/webcpu/deep-research-skill/main/deep-research/SKILL.md
```

## How it works

1. **Parse** — detects whether you gave a topic, a file path, or both
2. **Scope** — decides create vs. update mode; picks research angles
3. **Research** — launches parallel agents with `run_in_background: true`, each searching from a different angle
4. **Synthesize** — filters findings (drops anything without a source URL), groups by theme, writes the playbook
5. **Verify** — reads the result to check for duplicates, missing citations, and cohesion

## Output format

Every playbook follows this structure:

```markdown
# Topic Title

## Section Name
Insight text. — [Source Name](https://url)
Another insight. — [Another Source](https://url)

---
## Sources
- [Source 1](https://url)
- [Source 2](https://url)

---
*Captured: 2026-03-03*
```

Every claim is cited. No filler, no hedging.

## Updating an existing playbook

Point it at a file you've already created:

```
/deep-research --file agent-browser.md WebDriver BiDi protocol
```

It reads the existing content, launches agents focused on the new topic, and **merges** findings into the existing sections — matching the voice and style already in the document. It never overwrites or creates a separate "Updates" section.

## Requirements

- Claude Code with Opus

## License

MIT
