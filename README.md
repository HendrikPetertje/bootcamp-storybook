# React + TypeScript + Vite + Storybook

How to get here

## Base
- Install NPM and Yarn.

## Create a new app and start storybook

```sh
yarn create vite the-peter-way --template react-ts
```

## Inject storybook

```sh
npx storybook@latest init
```

## Prettier

```sh
yarn add -D eslint-config-prettier eslint-plugin-prettier prettier
```

## .prettierrc

```js
{
  "bracketSpacing": true,
  "endOfLine": "auto",
  "printWidth": 100,
  "singleQuote": true,
  "tabWidth": 2,
  "trailingComma": "all",
  "singleAttributePerLine": true
}
```

Add prettier to eslintrc too!

add little rule to package.json to deal with eslint being broken:
(remove `yarn.lock` and `node_modules`)

```js
  "resolutions": {
    "strip-ansi": "^6.0.1",
    "string-width": "^4.2.2",
    "wrap-ansi": "^7.0.0"
  }
```

yarn lint should succeed now

## Aliases

vite.config.ts

```ts
import * as path from 'path';
...

  css: {
    modules: {
      scopeBehaviour: 'local',
      generateScopedName: "[name]_[local]_[hash:8]",
    }
  },
  resolve: {
    alias: [
      // Base
      { find: "~base", replacement: path.resolve(__dirname, "./src/components/atomic/base") },

      // Atomic
      { find: "~atoms", replacement: path.resolve(__dirname, "./src/components/atomic/atoms") },
      { find: "~molecules", replacement: path.resolve(__dirname, "./src/components/atomic/molecules") },
      { find: "~organisms", replacement: path.resolve(__dirname, "./src/components/atomic/organisms") },
      { find: "~layouts", replacement: path.resolve(__dirname, "./src/components/atomic/layouts") },

      // Pages
      { find: "~pages", replacement: path.resolve(__dirname, "./src/components/pages") },

      // support infrastructure
      { find: "~services", replacement: path.resolve(__dirname, "./src/services") },
      { find: "~repositories", replacement: path.resolve(__dirname, "./src/repositories") },
      { find: "~config", replacement: path.resolve(__dirname, "./src/config") },

      // etc
      { find: "~components", replacement: path.resolve(__dirname, "./src/components") },
      { find: "~src", replacement: path.resolve(__dirname, "./src") },
      { find: "~root", replacement: path.resolve(__dirname, "./") },
    ]
  }
```

tsconfig

compiler-options:
```js
    "baseUrl": "./",
    "paths": {
      "~base/*": [ "./src/components/atomic/base/*" ],
      "~atoms/*": [ "./src/components/atomic/atoms/*" ],
      "~molecules/*": [ "./src/components/atomic/molecules/*" ],
      "~organisms/*": [ "./src/components/atomic/organisms/*" ],
      "~layouts/*": [ "./src/components/atomic/layouts/*" ],
      "~pages/*": [ "./src/components/pages/*" ],
      "~services/*": [ "./src/services/*" ],
      "~repositories/*": [ "./src/repositories/*" ],
      "~config/*": [ "./src/config/*" ],
      "~components/*": [ "./src/components/*" ],
      "~src/*": [ "./src/*" ],
      "~root/*": [ "./*" ]
    }
```

## Storybook config

Make sure we only see .stories.mdx as stories, so we don't have to deal 
with attempted rendering of support files in the `__stories` directory

main.ts
```ts
stories: ['../src/**/*.stories.mdx', '../src/**/*.stories.@(js|jsx|ts|tsx)'],
```

## Sass
yarn add -D sass

