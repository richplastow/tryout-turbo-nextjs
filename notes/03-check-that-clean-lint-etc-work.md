# Step 3: Check that `clean`, `lint`, `type-check` and `prettier` work

[^ Notes](./00-notes.md)

## Check that `clean` works

After the previous two steps, there's the top-level .turbo/ folder, and .next/
and .turbo/ folders in each of the two apps. The packages/ui/ library also has
.turbo/ and dist/ folders.

```bash
npm run clean
# > tryout-turbo-nextjs@0.0.1 clean
# > turbo clean
# • Packages in scope: @repo/eslint-config, @repo/tailwind-config, @repo/typescript-config, @repo/ui, docs, web
# • Running clean in 6 packages
# • Remote caching disabled
```

This doesn't seem to do much... TODO investigate

## Check that `lint` works

```bash
npm run lint
# > tryout-turbo-nextjs@0.0.1 lint
# > turbo lint
# • Packages in scope: @repo/eslint-config, @repo/tailwind-config, @repo/typescript-config, @repo/ui, docs, web
# • Running lint in 6 packages
# • Remote caching disabled
# ┌ @repo/ui#lint > cache hit (outputs already on disk), replaying logs d899e65e563e7965
# │ > @repo/ui@0.0.0 lint
# │ > eslint src/
# │ (node:73235) [ESLINT_PERSONAL_CONFIG_SUPPRESS] DeprecationWarning: '~/.eslintrc.*' config files ha
# │ ve been deprecated. Please remove it or add 'root:true' to the config files in your projects in or
# │ der to avoid loading '~/.eslintrc.*' accidentally. (found in "../../../../../../../.eslintrc")
# │ (Use `node --trace-deprecation ...` to show where the warning was created)
# └────>
# ┌ docs#lint > cache hit (outputs already on disk), replaying logs c7140283a3a8790f
# │ > docs@1.0.0 lint
# │ > next lint
# │ ...
# └────>
# ┌ web#lint > cache hit (outputs already on disk), replaying logs 1f50b52c2b202bc8
# │ > web@1.0.0 lint
# │ > next lint
# │ ...
# │ ✔ No ESLint warnings or errors
# └────>
```

No files are changed by this script. TODO break something and check that `lint` fixes it

## Check that `type-check` works

Since the apps build ok in the previous two steps, there's no reason to expect
that this would fail.

```bash
npm run type-check
# > tryout-turbo-nextjs@0.0.1 type-check
# > turbo type-check
# • Packages in scope: @repo/eslint-config, @repo/tailwind-config, @repo/typescript-config, @repo/ui, docs, web
# • Running type-check in 6 packages
# • Remote caching disabled
# ┌ @repo/ui#type-check > cache miss, executing be92f0ea4705c0fe
# │
# │ > @repo/ui@0.0.0 type-check
# │ > tsc --noEmit
# └────>
# ┌ docs#type-check > cache miss, executing 846d77b2857b24a0
# │
# │ > docs@1.0.0 type-check
# │ > tsc --noEmit
# └────>
# ┌ web#type-check > cache miss, executing a1cb9ebe4ce32e57
# │
# │ > web@1.0.0 type-check
# │ > tsc --noEmit
# └────>
```

No problems with TypeScript types.

## Check that `format` works

This actually runs `prettier`, under the hood.

```bash
npm run format
> tryout-turbo-nextjs@0.0.1 format
> prettier --write "**/*.{ts,tsx,md}"
# apps/docs/next-env.d.ts 242ms (unchanged)
# apps/docs/README.md 43ms (unchanged)
# apps/docs/src/app/layout.tsx 34ms (unchanged)
# apps/docs/src/app/page.tsx 45ms (unchanged)
# apps/docs/tailwind.config.ts 6ms (unchanged)
# apps/web/next-env.d.ts 2ms (unchanged)
# apps/web/README.md 13ms (unchanged)
# apps/web/src/app/layout.tsx 7ms (unchanged)
# apps/web/src/app/page.tsx 46ms (unchanged)
# apps/web/tailwind.config.ts 16ms (unchanged)
# notes/00-notes.md 12ms
# notes/01-install-turborepo.md 83ms
# notes/02-deploy-to-vercel.md 21ms (unchanged)
# notes/03-check-that-clean-lint-etc-work.md.md 8ms
# notes/appendix-1-turborepo-tailwind-starter-readme.md 27ms (unchanged)
# packages/config-eslint/README.md 6ms (unchanged)
# packages/config-tailwind/tailwind.config.ts 4ms (unchanged)
# packages/ui/src/card.tsx 6ms (unchanged)
# packages/ui/tailwind.config.ts 3ms (unchanged)
# README.md 6ms (unchanged)
```

The only files that needed to be formatted were Markdown, in notes/.
