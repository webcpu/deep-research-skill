# Deep Research

A Claude Code skill that researches any topic using parallel web search agents and produces a structured, source-cited playbook.

## What it does

1. You give it a topic
2. It launches 3-5 parallel research agents that search the web from different angles (official docs, community blogs, social media)
3. It synthesizes all findings into a single markdown playbook with source citations for every claim
4. It can also update an existing playbook with new findings

## Install

```bash
npx skills add your-username/deep-research-skill
```

Or manually:

```bash
mkdir -p ~/.claude/skills/deep-research
curl -o ~/.claude/skills/deep-research/SKILL.md \
  https://raw.githubusercontent.com/your-username/deep-research-skill/main/deep-research/SKILL.md
```

## Usage

```
/deep-research swift concurrency
/deep-research kubernetes cost optimization --file infra-playbook.md
/deep-research --file existing-playbook.md
```

- **Topic only**: creates `<topic-slug>.md` in your current directory
- **With `--file`**: writes to the specified path
- **Existing file**: updates it with new findings (merges, doesn't overwrite)

## Output

A markdown playbook with:
- Sections grouped by theme
- Every claim cited: `[Insight]. — [Source Name](URL)`
- A consolidated Sources list
- A `*Captured: YYYY-MM-DD*` timestamp

## Requirements

- Claude Code with web search enabled
- Works with Sonnet, Opus, and Haiku (Opus recommended for best results)

## License

MIT
