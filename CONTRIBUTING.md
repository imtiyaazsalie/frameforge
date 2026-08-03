# Contributing to Frameforge

Bug reports, fixes, new tools, docs, and ideas are all welcome. Keep interactions respectful and constructive.

This page covers the contribution process. The technical side (architecture, monorepo layout, tech stack, gotchas) lives in [AGENTS.md](./AGENTS.md), the canonical guide for working in this repo.

## Set up the repo

You need **Node.js 24 LTS or newer** (see [`.node-version`](./.node-version)) and **pnpm 11**. The pnpm version is pinned via `packageManager` in the root `package.json`, so [Corepack](https://nodejs.org/api/corepack.html) picks it up automatically.

```bash
git clone https://github.com/imtiyaazsalie/frameforge.git
cd frameforge
pnpm install
pnpm build
```

To run your local build end-to-end, point your MCP client at the built server and import the plugin from `packages/plugin`; the [Quick start](./README.md#quick-start) in the README walks through it. After changing `packages/mcp` or `packages/shared`, rebuild and restart the MCP server: it runs the built `dist`, not source.

## Run the checks

The same gates CI enforces on every push and PR run from the repo root:

```bash
pnpm typecheck && pnpm lint && pnpm format:check && pnpm knip && pnpm build && pnpm test
```

Things to know before your first PR (details in [AGENTS.md](./AGENTS.md)):

- **`pnpm test` from the root is canonical.** It picks up both `packages/*/test/**` and the cross-package suite in the root `test/`. Don't run tests per-package or you'll miss the integration tests.
- **No git hooks.** Formatting and lint are enforced by CI, so run `pnpm format` before committing (or format on save).
- **Tests live in `test/`**, mirroring `src/`; nothing is co-located. Cross-package tests go in the root `test/`.
- Add or update tests for any behavior change.

## Bugs, features, and pull requests

- **Report a bug** by opening an [issue](https://github.com/imtiyaazsalie/frameforge/issues) with steps to reproduce, what you expected, and what happened. Include your MCP client, OS, and Frameforge/Node versions.
- **Request a feature** by describing the problem you're trying to solve rather than a specific solution. Frameforge is provider-first and aims for generality, so proposals that make a wide range of real designs work better are prioritized over narrow, one-off additions.
- **Send a pull request**: for anything non-trivial, open an issue first so we can agree on the approach before you invest time.

## Commits and PR titles

- We use [Conventional Commits](https://www.conventionalcommits.org/): prefix messages with `feat:`, `fix:`, `chore:`, `refactor:`, `docs:`, `ci:`, etc. The version bump and changelog are derived from these.
- PR titles are validated (`semantic-pr.yml`) and must follow the same format. PRs are squash-merged, so the PR title becomes the commit on `main`; write it accordingly.
- Branch off `main`, keep PRs focused, and make sure CI is green before requesting review.

## Releasing

Maintainers handle releases. Versioning and the changelog are driven by Conventional Commits via `changelogen`; see [Releasing](./AGENTS.md#releasing) in AGENTS.md for the full flow.

## License

By contributing, you agree that your contributions are licensed under the project's [MIT License](./LICENSE).
