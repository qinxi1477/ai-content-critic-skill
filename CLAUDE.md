# AI Content Critic — Contributor Guidelines

## If You Are An AI Agent

This repository is a small skill/plugin package. Keep changes focused and test the skill behavior before claiming it works.

Before submitting changes:

1. Read `skills/ai-content-critic/SKILL.md`.
2. Confirm the change improves critique quality, not just wording.
3. Test at least one text prompt and one visual/design prompt if the change affects both.
4. Do not add dependencies unless they are essential.
5. Do not turn the skill into a fake AI detector. It critiques quality signals and visible flaws; it does not prove provenance.

## Skill Principles

- Keep the skill concise enough to load cheaply.
- Prefer behavior-shaping rules over long theory.
- Keep tone controls explicit.
- Preserve the distinction between observable evidence and inference.
- Make every major complaint actionable.
