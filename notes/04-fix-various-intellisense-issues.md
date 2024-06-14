# Step 4: Fix various IntelliSense issues

[^ Notes](./00-notes.md)

Currently `npm run lint/type-check/format` all work without errors or warnings.

But there are several kinds of errors and warnings that VS Code's [IntelliSense](https://code.visualstudio.com/docs/editor/intellisense) sees.

## Allow tsconfig.json files nested in apps/ and packages/

The apps/docs/src/app/layout.tsx file currently shows "Parsing error: Cannot
read file '/users/.../tsconfig.json' eslint" when you hover over the `import`
on line 1.

From <https://stackoverflow.com/a/64736676> change apps/docs/.eslintrc.js to:

```js
module.exports = {
  extends: ["@repo/eslint-config/next.js"],
  parserOptions: {
    project: "./tsconfig.json",
    tsconfigRootDir: __dirname,
  },
};
```

You should see that the error disappears, after a few seconds.

Repeat for the apps/web/.eslintrc.js and packages/ui/.eslintrc.js files.

## Allow `@tailwind` in .css files

The packages/ui/src/styles.css file currently shows "Unknown at rule
@tailwindcss(unknownAtRules)" when you hover over the `@tailwind` on line 1.

From <https://github.com/tailwindlabs/tailwindcss/discussions/5258#discussioncomment-1979394>
create the .vscode/ folder, containing a settings.json file:

```bash
mkdir .vscode
echo '{ "css.customData": [".vscode/tailwind.json"] }' > .vscode/settings.json
```

And then create the .vscode/tailwind.json file:

````json
{
  "version": 1.1,
  "atDirectives": [
    {
      "name": "@tailwind",
      "description": "Use the `@tailwind` directive to insert Tailwind's `base`, `components`, `utilities` and `screens` styles into your CSS.",
      "references": [
        {
          "name": "Tailwind Documentation",
          "url": "https://tailwindcss.com/docs/functions-and-directives#tailwind"
        }
      ]
    },
    {
      "name": "@apply",
      "description": "Use the `@apply` directive to inline any existing utility classes into your own custom CSS. This is useful when you find a common utility pattern in your HTML that you’d like to extract to a new component.",
      "references": [
        {
          "name": "Tailwind Documentation",
          "url": "https://tailwindcss.com/docs/functions-and-directives#apply"
        }
      ]
    },
    {
      "name": "@responsive",
      "description": "You can generate responsive variants of your own classes by wrapping their definitions in the `@responsive` directive:\n```css\n@responsive {\n  .alert {\n    background-color: #E53E3E;\n  }\n}\n```\n",
      "references": [
        {
          "name": "Tailwind Documentation",
          "url": "https://tailwindcss.com/docs/functions-and-directives#responsive"
        }
      ]
    },
    {
      "name": "@screen",
      "description": "The `@screen` directive allows you to create media queries that reference your breakpoints by **name** instead of duplicating their values in your own CSS:\n```css\n@screen sm {\n  /* ... */\n}\n```\n…gets transformed into this:\n```css\n@media (min-width: 640px) {\n  /* ... */\n}\n```\n",
      "references": [
        {
          "name": "Tailwind Documentation",
          "url": "https://tailwindcss.com/docs/functions-and-directives#screen"
        }
      ]
    },
    {
      "name": "@variants",
      "description": "Generate `hover`, `focus`, `active` and other **variants** of your own utilities by wrapping their definitions in the `@variants` directive:\n```css\n@variants hover, focus {\n   .btn-brand {\n    background-color: #3182CE;\n  }\n}\n```\n",
      "references": [
        {
          "name": "Tailwind Documentation",
          "url": "https://tailwindcss.com/docs/functions-and-directives#variants"
        }
      ]
    }
  ]
}
````

You should see that the warnings disappear, probably after restarting VS Code.
