# karpathy-guidelines-skill

Codex skill for cautious software development with explicit assumptions, simple solutions, surgical edits, and clear verification.

## What This Is

This repository packages a Codex skill named `karpathy-guidelines`.

Use it when you want coding tasks to follow a stricter engineering style:

- think before coding
- prefer simplest solution that works
- make surgical changes only
- verify against clear goals

## Files

- `SKILL.md`: skill trigger description and working rules
- `agents/openai.yaml`: UI metadata for Codex skill discovery

## Install

Copy this repository into your Codex skills directory:

```bash
mkdir -p "${CODEX_HOME:-$HOME/.codex}/skills"
cp -R karpathy-guidelines-skill "${CODEX_HOME:-$HOME/.codex}/skills/"
```

If you want skill folder name to match skill name exactly, rename copied folder to `karpathy-guidelines`.

## Use

Reference it explicitly in prompts:

```text
Use $karpathy-guidelines to debug this regression with minimal code changes.
```

Typical use cases:

- implement feature without over-engineering
- debug bug with explicit assumptions
- refactor code while preserving behavior
- review patch for regressions and missing verification

## Principles

1. Think before coding.
2. Keep code simple.
3. Make surgical edits.
4. Verify against goal.
