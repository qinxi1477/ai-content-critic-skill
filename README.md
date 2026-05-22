# AI Content Critic

A blunt but evidence-based critique skill for spotting AI slop in text, images, slides, posters, and UI — then turning it into concrete fixes.

AI Content Critic is a cross-agent skill for Claude Code and Codex that reviews AI-generated text, images, slides, posters, UI screenshots, and mixed media.

[中文说明](README.zh-CN.md)

This skill does not prove authorship. It diagnoses quality signals that often make content feel synthetic, generic, visually broken, or untrustworthy.

## What It Does

- Finds AI tells in articles, essays, reports, posts, and marketing copy
- Calls out bland writing, weak logic, fake specificity, unsupported claims, and repetitive structure
- Reviews generated images for anatomy, text, lighting, perspective, edge, material, and scene-coherence defects
- Reviews slides, posters, and UI for hierarchy, density, typography, alignment, visual proof, and template smell
- Supports several critique tones: gentle, direct, roast, mentor, and client-ready
- Keeps criticism evidence-based instead of making unsupported claims that something was definitely AI-generated

## Quickstart

Install the skill for the agent you use.

### Claude Code

Project-local install:

```bash
mkdir -p .claude/skills
cp -R skills/ai-content-critic .claude/skills/
```

Personal install:

```bash
mkdir -p ~/.claude/skills
cp -R skills/ai-content-critic ~/.claude/skills/
```

Then ask Claude Code:

```text
/ai-content-critic review this generated poster and be blunt
```

Claude Code skills are filesystem artifacts with a required `SKILL.md`; project skills live under `.claude/skills/<name>/SKILL.md`, and personal skills live under `~/.claude/skills/<name>/SKILL.md`.

### Codex

Personal install:

```bash
mkdir -p ~/.codex/skills
cp -R skills/ai-content-critic ~/.codex/skills/
```

If you publish this repository as a Codex plugin, the `codex-plugin/plugin.json` manifest points Codex at `./skills/`.

Then ask Codex:

```text
Use $ai-content-critic to roast this AI-generated article and give me a rewrite plan.
```

## Verify Installation

After installing, start a fresh agent session and ask:

```text
What skills are available?
```

Or invoke it directly:

```text
Use ai-content-critic to review this one-sentence sample: "In today's fast-paced world, innovation is more important than ever."
```

Expected result: the agent should mention `ai-content-critic` or respond with a critique that follows the skill's verdict/issues/fixes structure.

If the skill is not found:

- Confirm `skills/ai-content-critic/SKILL.md` exists in this repository.
- For Claude Code project installs, confirm it was copied to `.claude/skills/ai-content-critic/SKILL.md`.
- For Claude Code personal installs, confirm it was copied to `~/.claude/skills/ai-content-critic/SKILL.md`.
- For Codex personal installs, confirm it was copied to `~/.codex/skills/ai-content-critic/SKILL.md`.
- Restart the agent session if the skill directory did not exist when the session began.
- If installing as a plugin, confirm `.codex-plugin/plugin.json` or `claude-plugin/plugin.json` is present in the repository and that the manifest points to `./skills/`.

## Example Prompts

```text
Use ai-content-critic to review this article. Tell me which parts feel AI-written and what to cut.
```

```text
Use ai-content-critic on this image. Roast it first, then give me a retouch or regeneration plan.
```

```text
Use ai-content-critic to review these slides for AI slop, weak hierarchy, and unreadable details.
```

```text
Use ai-content-critic in client-ready mode. No jokes, just issues and fixes.
```

See the `examples/` directory for sample review formats:

- `examples/text-review.md`
- `examples/image-review.md`
- `examples/slide-review.md`
- `examples/roast-mode.md`
- `examples/client-ready-mode.md`

## Output Style

The skill usually returns:

1. A short verdict
2. A prioritized list of visible or textual defects
3. Why the artifact reads as AI-generated or low-quality
4. Concrete fixes, rewrite directions, or retouch/regeneration steps

When the user asks for `吐槽`, `锐评`, `毒舌`, `别客气`, or `roast`, the critique gets sharper, but the repair advice stays practical.

## Repository Layout

```text
.
├── claude-plugin/
│   └── plugin.json
├── codex-plugin/
│   └── plugin.json
├── examples/
│   ├── client-ready-mode.md
│   ├── image-review.md
│   ├── roast-mode.md
│   ├── slide-review.md
│   └── text-review.md
├── skills/
│   └── ai-content-critic/
│       └── SKILL.md
├── AGENTS.md
├── CLAUDE.md
├── LICENSE
├── README.md
├── README.zh-CN.md
└── package.json
```

## Philosophy

- Evidence over vibes
- Specific fixes over generic advice
- Critique the artifact, not the person
- "Looks AI-generated" is a diagnosis of quality signals, not proof of provenance
- Funny is allowed; careless is not

## License

MIT License. See `LICENSE`.

## Citation

If you use this skill in research workflows, paper writing, poster review, or benchmark artifact review, please cite this repository.
