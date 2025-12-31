# Contribution Guide

Thanks for your interest in contributing to [my projects](https://github.com/gmickel?tab=repositories). Please read this before submitting your contribution.

## Repository Setup

I use [Bun](https://bun.sh/) or [pnpm](https://pnpm.io/) depending on the project. I recommend installing [@antfu/ni](https://github.com/antfu/ni) so you don't need to worry about package managers when switching projects.

| Step | Command |
|------|---------|
| 1. Install [Node.js LTS](https://nodejs.org/) | - |
| 2. Enable [Corepack](https://nodejs.org/api/corepack.html) | `corepack enable` |
| 3. Install [Bun](https://bun.sh/docs/installation) | `curl -fsSL https://bun.sh/install \| bash` |
| 4. Install [@antfu/ni](https://github.com/antfu/ni) | `npm i -g @antfu/ni` |
| 5. Install dependencies | `ni` |
| 6. Install git hooks | `nlx lefthook install` |

With ni: `ni` = install, `nr` = run, `nlx` = execute. It auto-detects the package manager from lockfile.

## Commands

| Command | Description |
|---------|-------------|
| `nr dev` | Start dev server/environment |
| `nr build` | Build for production |
| `nr test` | Run tests (Vitest or Bun test) |
| `nr test --watch` | Run tests in watch mode |
| `nr lint` | Lint and format check |
| `nr lint:fix` | Auto-fix lint/format issues |
| `nr typecheck` | Type check with tsc/tsgo |

Run bare `nr` to see all available scripts.

### Testing

I use [Vitest](https://vitest.dev/) or Bun's built-in test runner. Filter tests: `nr test foo`. Run once: `nr test --run`. UI mode: `nr test --ui`.

## Linting & Formatting

I use [Biome](https://biomejs.dev/) for linting and formatting (often via [ultracite](https://github.com/haydenbleasel/ultracite)). Biome handles JS/TS, JSON, and more in a single fast tool.

**No Prettier** - Biome handles formatting. Disable Prettier in your editor for these projects.

### Git Hooks

Most projects use [Lefthook](https://github.com/evilmartians/lefthook) for pre-commit hooks that auto-format staged files.

### IDE Setup

Use [VS Code](https://code.visualstudio.com/) or your preferred fork with the [Biome extension](https://marketplace.visualstudio.com/items?itemName=biomejs.biome). Projects include `.vscode/settings.json` for format-on-save.

## Pull Requests

### Discuss First

Open an issue before starting significant work. Helps align on design and saves time.

### Commit Convention

I use [Conventional Commits](https://www.conventionalcommits.org/):

- `feat:` - new features
- `fix:` - bug fixes
- `docs:` - documentation only
- `chore:` - maintenance, deps, etc.

Only `fix:` and `feat:` appear in changelogs. Use `docs: fix typo` not ~~`fix: typo`~~.

### Submitting

1. PR title follows commit convention
2. Link issues: `fix #123` in description
3. Multiple commits fine - I squash merge

If new to PRs, see [GitHub's guide](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request).

## Monorepos

Some projects use [Turborepo](https://turbo.build/repo) for monorepo management.
