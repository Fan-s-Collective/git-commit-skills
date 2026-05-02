# git-commit-skill

An agent skill for writing Conventional Commit messages from staged or unstaged git changes.

## What It Does

`git-commit-skill` helps an AI coding agent inspect Git changes and produce a concise commit message that follows the Conventional Commits format.

It is useful when you want commit messages that are:

- grounded in the actual repository diff
- written in a consistent Conventional Commits style
- concise enough for everyday development
- clear about the changed behavior or project metadata

## Package

This repository is published as a normal npm package while its primary payload is an agent skill.

```sh
pnpm add git-commit-skill
```

The package is intended to ship skill files such as `SKILL.md` and related agent resources.

## Conventional Commits

Generated messages should follow this shape:

```text
type(scope): summary
```

Examples:

```text
docs: add README for git commit skill
chore(package): describe package as an agent skill
```

## License

MIT
