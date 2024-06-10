# Step 1: Install `turbo` and the Next.js + Tailwind starter

[^ Notes](./00-notes.md)

> _“Turbo is an incremental bundler and build system optimized for JavaScript_
> _and TypeScript, written in Rust.”_ - <https://turbo.build/>

## Install `turbo` globally

```bash
turbo --version
# -bash: turbo: command not found
npm i --global turbo
# added 2 packages in 2s
turbo --version
# No locally installed `turbo` found. Using version: 2.0.3.
# 2.0.3
```

## Install `with-tailwind`, the Next.js + Tailwind starter

Turbo publishes a [list of recommended starters,](
https://turbo.build/repo/docs/getting-started/installation#start-with-an-example)
and several use the Next.js React framework. I had encountered issues trying to
use Tailwind with `@nx/vite` and `@nx/next` (Nx is an alternative monorepo), so
I was interested to see if Turbo's Tailwind worked any better.

Following the <https://github.com/vercel/turbo/tree/main/examples/with-tailwind>
README:

```bash
npx create-turbo@latest -e with-tailwind
# Need to install the following packages:
# create-turbo@2.0.3
# Ok to proceed? (y)
y
# npm WARN deprecated inflight@1.0.6: ...
# npm WARN deprecated rimraf@3.0.2: ...
# npm WARN deprecated glob@7.2.3: ...
# >>> TURBOREPO
# >>> Welcome to Turborepo! Let's get you set up with a new codebase.
# ? Where would you like to create your turborepo? (./my-turborepo)
./my-turborepo
# ? Which package manager do you want to use? (Use arrow keys)
# ❯ npm workspaces
#   - pnpm workspaces (not installed)
#   yarn workspaces
#   - bun workspaces (beta) (not installed)
npm workspaces
# Downloading files for example with-tailwind. This might take a moment.
# >>> Created a new Turborepo with the following:
# apps
#  - apps/docs
#  - apps/web
# packages
#  - packages/config-eslint
#  - packages/config-tailwind
#  - packages/config-typescript
#  - packages/ui
# Installing packages. This might take a couple of minutes.

```

