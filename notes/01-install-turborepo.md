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
# >>> Success! Created a new Turborepo at "my-turborepo".
# Inside that directory, you can run several commands:
#   npm run build
#      Build all apps and packages
#   npm run dev
#      Develop all apps and packages
#   npm run lint
#      Lint all apps and packages
# Turborepo will cache locally by default. For an additional
# speed boost, enable Remote Caching with Vercel by
# entering the following command:
#   npx turbo login
# We suggest that you begin by typing:
#   cd my-turborepo
#   npx turbo login
```

On my macOS, the new my-turborepo/ folder is 348,971,971 bytes (426.3 MB on
disk) for 26,276 items. Its node_modules/ folder is 348,747,864 bytes (425.9 MB
on disk) for 26,208 items.

## Check that `dev` is working

```bash
cd my-turborepo
npm run dev
# > dev
# > turbo dev
# Attention:
# Turborepo now collects completely anonymous telemetry regarding usage.
# This information is used to shape the Turborepo roadmap and prioritize features.
# You can learn more, including how to opt-out if you'd not like to participate in this anonymous program, by visiting the following URL:
# https://turbo.build/repo/docs/telemetry
# • Packages in scope: @repo/eslint-config, @repo/tailwind-config, @repo/typescript-config, @repo/ui, docs, web
# • Running dev in 6 packages
# • Remote caching disabled
# Task          ┌ @repo/ui#dev > cache bypass, force executing f9a5eb0aba7fb097 ───────────────────────────────────┐
# ──────────────│                                                                                                  │
# @repo/ui#dev ⠴│> @repo/ui@0.0.0 dev                                                                              │
# web#dev      ⠴│> tailwindcss -i ./src/styles.css -o ./dist/index.css --watch                                     │
# docs#dev     ⠴│                                                                                                  │
#               │                                                                                                  │
#               │Rebuilding...                                                                                     │
#               │                                                                                                  │
#               │Done in 1200ms.                                                                                   │
#               │                                                                                                  │
#               └Use arrow keys to navigate. Press `Enter` to interact with a task and `Ctrl-Z` to stop interacting┘
[down-arrow]
# Task          ┌ web#dev > cache bypass, force executing 8e299dd128ea2c49 ────────────────────────────────────────┐
# ──────────────│                                                                                                  │
# @repo/ui#dev ⠦│> web@1.0.0 dev                                                                                   │
# web#dev      ⠦│> next dev                                                                                        │
# docs#dev     ⠦│                                                                                                  │
#               │  ▲ Next.js 14.2.3                                                                                │
#               │  - Local:        http://localhost:3000                                                           │
#               │                                                                                                  │
#               │ ✓ Starting...                                                                                    │
#               │ ✓ Ready in 12.4s                                                                                 │
#               │                                                                                                  │
#               └Use arrow keys to navigate. Press `Enter` to interact with a task and `Ctrl-Z` to stop interacting┘
[down-arrow]
# Task          ┌ docs#dev > cache bypass, force executing f738cd99f6013591 ───────────────────────────────────────┐
# ──────────────│                                                                                                  │
# @repo/ui#dev ⠸│> docs@1.0.0 dev                                                                                  │
# web#dev      ⠸│> next dev --port 3001                                                                            │
# docs#dev     ⠸│                                                                                                  │
#               │  ▲ Next.js 14.2.3                                                                                │
#               │  - Local:        http://localhost:3001                                                           │
#               │                                                                                                  │
#               │ ✓ Starting...                                                                                    │
#               │ ✓ Ready in 12.2s                                                                                 │
#               │                                                                                                  │
#               └Use arrow keys to navigate. Press `Enter` to interact with a task and `Ctrl-Z` to stop interacting┘
```

Visit <http://localhost:3000> to see the default turborepo page showing
"examples/with-tailwind - web", and <http://localhost:3001> to see it showing
"examples/with-tailwind - docs".

## Check that `lint` is working

```bash
npm run lint
# > lint
# > turbo lint
# • Packages in scope: @repo/eslint-config, @repo/tailwind-config, @repo/typescript-config, @repo/ui, docs, web
# • Running lint in 6 packages
# • Remote caching disabled
# Task            ┌ @repo/ui#lint > cache miss, executing d899e65e563e7965 ────────────────────────────────────────┐
# ────────────────│                                                                                                │
# web#lint       ⠇│> @repo/ui@0.0.0 lint                                                                           │
# docs#lint      ⠇│> eslint src/                                                                                   │
# @repo/ui#lint  ⠇│                                                                                                │
#                 │                                                                                                │
#                 └Use arrow keys to navigate. Press `Enter` to interact with a task and `Ctrl-Z` to stop interacti┘
[down-arrow]
# ...
```

After a short wait, the interactive TUI will quit, reporting that there are no
lint problems.

## Check that `build` is working

```bash
npm run build
# > build
# > turbo build
# • Packages in scope: @repo/eslint-config, @repo/tailwind-config, @repo/typescript-config, @repo/ui, docs, web
# • Running build in 6 packages
# • Remote caching disabled
# Task             ┌ @repo/ui#build > cache miss, executing 9cd5976763dde1d7 ──────────────────────────────────────┐
# ─────────────────│                                                                                               │
# @repo/ui#build  ✔│> @repo/ui@0.0.0 build                                                                         │
# web#build       ⠋│> tailwindcss -i ./src/styles.css -o ./dist/index.css                                          │
# docs#build      ⠋│                                                                                               │
#                  │                                                                                               │
#                  │Rebuilding...                                                                                  │
#                  │                                                                                               │
#                  │Done in 1024ms.                                                                                │
#                  │                                                                                               │
#                  └Use arrow keys to navigate. Press `Enter` to interact with a task and `Ctrl-Z` to stop interact┘
[down-arrow]
# Task             ┌ web#build > cache miss, executing ba68ecd413a5aa40 ───────────────────────────────────────────┐
# ─────────────────│                                                                                               │
# @repo/ui#build  ✔│> web@1.0.0 build                                                                              │
# web#build       ⠹│> next build                                                                                   │
# docs#build      ⠹│                                                                                               │
#                  │  ▲ Next.js 14.2.3                                                                             │
#                  │                                                                                               │
#                  │   Creating an optimized production build ...                                                  │
#                  │                                                                                               │
#                  └Use arrow keys to navigate. Press `Enter` to interact with a task and `Ctrl-Z` to stop interact┘
[down-arrow]
# Task             ┌ docs#build > cache miss, executing 4a1bd0e08afe53b9 ──────────────────────────────────────────┐
# ─────────────────│/.eslintrc.*' config files have been deprecated. Please remove it or add 'root:true' to the con│
# @repo/ui#build  ✔│g files in your projects in order to avoid loading '~/.eslintrc.*' accidentally. (found in "../│
# docs#build      ✔│/../../../../../.eslintrc")                                                                    │
# web#build       ⠸│(Use `node --trace-deprecation ...` to show where the warning was created)                     │
#                  │ ✓ Collecting page data                                                                        │
#                  │ ✓ Generating static pages (5/5)                                                               │
#                  │ ✓ Collecting build traces                                                                     │
#                  │ ✓ Finalizing page optimization                                                                │
#                  │                                                                                               │
#                  │Route (app)                              Size     First Load JS                                │
#                  │┌ ○ /                                    5.27 kB        92.2 kB                                │
#                  │└ ○ /_not-found                          876 B          87.8 kB                                │
#                  │+ First Load JS shared by all            87 kB                                                 │
#                  │  ├ chunks/1dd3208c-423052682a96d096.js  53.7 kB                                               │
#                  │  ├ chunks/286-6a0cbe5aa43df90a.js       31.5 kB                                               │
#                  │  └ other shared chunks (total)          1.85 kB                                               │
#                  │                                                                                               │
#                  │                                                                                               │
#                  │○  (Static)  prerendered as static content                                                     │
#                  │                                                                                               │
#                  └Use arrow keys to navigate. Press `Enter` to interact with a task and `Ctrl-Z` to stop interact┘
```

On my macOS, the new my-turborepo/ folder has grown to 442,781,402 bytes
(523.6 MB on disk) for 26,278 items (invisible files add to bytes and disk size,
but not number of items). Its node_modules/ folder is unchanged on 348,747,864
bytes (425.9 MB on disk) for 26,208 items.

