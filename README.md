# git-commit-skill

An agent skill for generating Conventional Commits-style git commit messages from real repository changes.

It helps coding agents inspect staged or unstaged diffs, infer the right commit intent, and produce a concise commit message grounded in the current repository instead of generic templates.

## Install & Upgrade

Install with the Skills CLI:

```bash
npx skills add Fan-s-Collective/git-commit-skills
```

Install only this skill explicitly:

```bash
npx skills add Fan-s-Collective/git-commit-skills --skill git-commit
```

Install globally so it is available across projects:

```bash
npx skills add Fan-s-Collective/git-commit-skills --skill git-commit --global
```

### Source Formats

```bash
# GitHub shorthand
npx skills add Fan-s-Collective/git-commit-skills

# Full GitHub URL
npx skills add https://github.com/Fan-s-Collective/git-commit-skills

# Direct path to the skill
npx skills add https://github.com/Fan-s-Collective/git-commit-skills/tree/main/skills/git-commit

# Any git URL
npx skills add git@github.com:Fan-s-Collective/git-commit-skills.git

# Local checkout
npx skills add ./git-commit-skills
```

### Options

| Option | Description |
| --- | --- |
| `-g, --global` | Install to the user skill directory instead of the current project |
| `-a, --agent <agents...>` | Install for specific agents, such as `codex`, `claude-code`, `cursor`, or `opencode` |
| `-s, --skill <skills...>` | Install specific skills by name, or use `'*'` for all skills |
| `-l, --list` | List available skills without installing |
| `--copy` | Copy files instead of symlinking them |
| `-y, --yes` | Skip confirmation prompts |
| `--all` | Install all skills to all agents without prompts |

## Usage

Ask your coding agent to use the skill when you need a commit message:

```text
Use $git-commit to generate a commit message for my current changes.
```

You can also be more specific:

```text
Use $git-commit to write a commit message from staged changes only.
```

```text
Use $git-commit to review this commit message and make it follow the repo convention.
```

The skill instructs the agent to:

- inspect `git status --short`
- prefer `git diff --staged` when staged changes exist
- use `git diff` for unstaged changes when needed
- read local commit convention files such as `CONTRIBUTING.md` or `COMMIT_CONVENTION.md`
- choose a Conventional Commits type and repository-specific scope
- add a body only when it clarifies intent, impact, compatibility, or mixed change types

## Output Format

The generated header follows Conventional Commits:

```text
<type>(<scope>): <subject>
```

Examples:

```text
docs(readme): document git commit skill usage
```

```text
chore: align package metadata for skill publishing
```

For mixed or higher-impact changes, the skill may include a body:

```text
refactor: align release workflow

- refactor: clarify build and publish responsibilities
- docs: document the updated release process
```

## Troubleshooting

### No Skills Found

Make sure the repository contains `skills/git-commit/SKILL.md` and that the file has valid YAML frontmatter with both `name` and `description`.

### Skill Not Loading

Verify that the skill was installed to the directory used by your agent. For Codex, project skills are usually installed under `.agents/skills/`, and global skills under `~/.codex/skills/`.

### Generic Commit Messages

Ask the agent to inspect the current diff again, and check whether your repository has a local commit convention file. This skill is designed to derive scope and wording from the actual changed paths and local project conventions.

## Related Links

- [Agent Skills Specification](https://agentskills.io)
- [Skills Directory](https://skills.sh)
- [Skills CLI README](https://github.com/vercel-labs/skills/blob/main/README.md)
- [Conventional Commits](https://www.conventionalcommits.org/)
- [Codex Skills Documentation](https://developers.openai.com/codex/skills)

## License

MIT
