# /deep-research

Google gives you sources but no synthesis — you drown in tabs. ChatGPT gives you synthesis but no sources — you can't verify anything, and it vanishes when you close the window.

This skill gives you both. One command, one markdown file where every claim links back to its source.

```
/deep-research Dario Amodei's vision for AI safety
```

You get a structured playbook you can keep, share, and update later.

> **Heads up:** Each run launches 3-5 parallel Opus agents. Token usage is higher than you'd expect. Best suited for **Claude Max subscribers**.

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
npx skills add webcpu/deep-research-skill -a claude-code --global
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

## Example output

`/deep-research Apple Studio Display XDR` produced a 14-section playbook with 36 sources and ~65 integrated findings:

- What It Is — Overview, pricing, availability
- Display Specifications — Full comparison table (XDR vs Studio Display vs Pro Display XDR)
- Configurations and Pricing — All SKUs, nano-texture analysis
- Connectivity — Thunderbolt 5, daisy-chaining, charging watts
- 120Hz Compatibility — Which Macs get 120Hz vs 60Hz
- Professional Reference Modes — 16 built-in presets, custom modes, DICOM medical imaging
- Camera, Audio, and Edge Light — Webcam history, speakers, virtual ring light
- The Pro Display XDR Trade-Off — Gains and losses vs the discontinued 32" model
- Known Issues and Gotchas — Stand lock-in, power cable, cable length, thermal throttling, firmware bricking, sleep/wake bugs
- Alternatives and Competitors — 6 alternatives with pricing
- Who Should Buy What — Decision framework by use case and Mac chip
- Calibration and Color Accuracy — Factory deltaE data, hardware calibration
- Compatibility Requirements — OS and hardware requirements
- Environmental — Recycled materials

See the full output: [examples/apple-studio-display-xdr.md](examples/apple-studio-display-xdr.md)

## Updating an existing playbook

Point it at a file you've already created:

```
/deep-research --file agent-browser.md WebDriver BiDi protocol
```

It reads the existing content, launches agents focused on the new topic, and **merges** findings into the existing sections — matching the voice and style already in the document. It never overwrites or creates a separate "Updates" section.

## Requirements

- Claude Code with Opus
- **Claude Max recommended** — each run launches 3-5 parallel Opus agents. Token usage is higher than you'd expect.

## License

MIT
