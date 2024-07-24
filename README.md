# Contribution Guide

Hey there! I am really excited that you are interested in contributing. This is a general contribution guide for most of [my projects](https://github.com/gmickel?tab=repositories). Before submitting your contribution, please make sure to take a moment and read through the following guide:

## 👨‍💻 Repository Setup

I use [ `pnpm` ](https://pnpm.io/) or [ `bun` ](https://bun.sh/) for most of the projects. I highly recommend you install [ `ni` ](https://github.com/antfu/ni) so you don't need to worry about the package manager when switching across different projects.

I will use `ni` 's commands in the following code snippets. If you are not using it, you can do the conversion yourself: `ni = pnpm/bun install` , `nr = pnpm/bun run` .

To set the repository up:

| Step | Command |
|-------|--------|
| 1. Install [Node.js](https://nodejs.org/), using the [latest LTS](https://nodejs.org/en/about/releases/) | - |
| 2. [Enable Corepack](#corepack) | `corepack enable` |
| 3. Install [ `@antfu/ni` ](https://github.com/antfu/ni) | `npm i -g @antfu/ni` |
| 4. Install dependencies under the project root | `ni` |

### Bun

Bun is not supported by corepack, so you need to install it manually. Refer to the [Bun documentation](https://bun.sh/docs/installation) for more information.

## 💡 Commands

### `nr dev`

Start the development environment.

If it's a frontend project, it usually starts the dev server. You can then develop and see the changes in real time.

### `nr play`

If it's a Node.js package, it starts a dev server for the playground. The code is usually under `playground/` .

### `nr build`

Build the project for production. The result is usually under `dist/` .

### `nr lint`

I use [ESLint](https://eslint.org/) or [Biome](https://biomejs.dev/) for **both linting and formatting**. They also lint JSON, YAML, and Markdown files if they exist.

You can run `nr lint --fix` to let ESLint format and lint the code.

Learn more about the [ESLint Setup](#eslint) and the [Biome Setup](#biome).

[**I don't usually use Prettier**](#no-prettier).

### `nr test`

Run the tests. I mostly use [Vitest](https://vitest.dev/) - a replacement for [Jest](https://jestjs.io/).

You can filter the tests to be run by `nr test [match]` , for example, `nr test foo` will only run test files that contain `foo` .

Config options are often under the `test` field of `vitest.config.ts` or `vite.config.ts` .

Vitest runs in [watch mode by default](https://vitest.dev/guide/features.html#watch-mode), so you can modify the code and see the test result automatically, which is great for [test-driven development](https://en.wikipedia.org/wiki/Test-driven_development). To run the test only once, you can do `nr test --run` .

For some projects, I might have multiple types of tests set up. For example `nr test:unit` for unit tests, `nr test:e2e` for end-to-end tests. `nr test` commonly runs them together, but you can run them separately as needed.

Vitest also has a UI mode which you can run with `nr test --ui` or `nr test:ui` in most projects.

### `nr docs`

If the project contains documentation, you can run `nr docs` to start the documentation dev server. Use `nr docs:build` to build the docs for production.

### `nr`

For more, you can run bare `nr` , which will prompt a list of all available scripts.

## 🙌 Sending Pull Request

### Discuss First

Before you start to work on a feature pull request, it's always better to open a feature request issue first to discuss with the maintainers whether the feature is desired and the design of those features. This would help save time for both the maintainers and the contributors and help features to be shipped faster.

For typo fixes, it's recommended to batch multiple typo fixes into one pull request to maintain a cleaner commit history.

### Commit Convention

I use [Conventional Commits](https://www.conventionalcommits.org/) for commit messages, which allows the changelog to be auto-generated based on the commits. Please read the guide through if you aren't familiar with it already.

Only `fix:` and `feat:` will be presented in the changelog.

Note that `fix:` and `feat:` are for **actual code changes** (that might affect logic).
For typo or document changes, use `docs:` or `chore:` instead:

* ~~`fix: typo`~~ -> `docs: fix typo`

### Pull Request

If you don't know how to send a Pull Request, I recommend reading [the guide](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request).

When sending a pull request, make sure your PR's title also follows the [Commit Convention](#commit-convention).

If your PR fixes or resolves an existing issue, please add the following line in your PR description (replace `123` with a real issue number):

```markdown
fix #123
```

This will let GitHub know the issues are linked, and automatically close them once the PR gets merged. Learn more at [the guide](https://docs.github.com/en/issues/tracking-your-work-with-issues/linking-a-pull-request-to-an-issue#linking-a-pull-request-to-an-issue-using-a-keyword).

It's ok to have multiple commits in a single PR, you don't need to rebase or force push for your changes as I will use `Squash and Merge` to squash the commits into one commit when merging.

## 📖 References

### Corepack

#### TL; DR

To enable it, run

```bash
corepack enable
```

You only need to do it once after Node.js is installed.

<table><tr><td width="500px" valign="top">

#### What's Corepack

[Corepack](https://nodejs.org/api/corepack.html) makes sure you are using the correct version for package manager when you run corresponding commands. Projects might have `packageManager` field in their `package.json` .

Under projects with configuration as shown on the right, corepack will install `v9.5.0` of `pnpm` (if you don't have it already) and use it to run your commands. This makes sure everyone working on this project has the same behavior for the dependencies and the lockfile.

</td><td width="500px"><br>

 `package.json`

```jsonc
{
  "packageManager": "pnpm@9.5.0"
}
```

</td></tr></table>

### ESLint

I use [ESLint](https://eslint.org/) for both linting and formatting with [ `@antfu/eslint-config` ](https://github.com/antfu/eslint-config).

### Biome

I use [Biome](https://biomejs.dev/) for both linting and formatting with a custom [configuration](https://biomejs.dev/reference/configuration/).

### IDE Setup

I recommend using [VS Code](https://code.visualstudio.com/) along with the [ESLint extension](https://marketplace.visualstudio.com/items?itemName=dbaeumer.vscode-eslint) or the [Biome extension](https://marketplace.visualstudio.com/items?itemName=biomejs.biome).

With the appropriate settings, you can have auto fix and formatting when you save the code you are editing.

I usually include a minimal `.vscode/settings.json` file that configures the correct extension for the specific project.

### No Prettier

Since ESLint is already configured to format the code, there is no need to duplicate the functionality with Prettier. To format the code, you can run `nr lint --fix` or refer to the [ESLint section](#eslint) for IDE Setup.

If you have Prettier installed in your editor, I recommend you disable it when working on the project to avoid conflicts.

### Turborepo

I use [Turborepo](https://github.com/vercel/turborepo) for monorepo management. It's a great tool for managing multiple packages in a single repository. You can read more about it [here](https://turbo.build/repo).

## 🙏🏽 Acknowledgements

This guide is heavily inspired by [Anthony Fu's contribution guide](https://github.com/antfu/contribution-guide).
