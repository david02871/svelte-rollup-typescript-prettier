# Svelte with Rollup, TypeScript & Prettier

Currently working with vscode extension "Svelte Beta".

```bash
git clone https://github.com/david02871/svelte-rollup-typescript-prettier.git
```

## To replicate without cloning
#### 1. Generate Svelte app using npx
```bash
npm install -g npx
npx degit sveltejs/template my-app-name
cd my-app-name
```

#### 2. Add developer dependencies
```bash
npm install --save-dev typescript tslib
npm install --save-dev svelte-preprocess @pyoner/svelte-ts-preprocess
npm install --save-dev @rollup/plugin-typescript
npm install --save-dev prettier prettier-plugin-svelte
```

#### 3. Rename /src/main.js to /src/main.ts

#### 4. Edit rollup.config.js:
Add imports:
```js
import typescript from "@rollup/plugin-typescript";
import preprocess from 'svelte-preprocess';
```

Change `input: 'src/main.js'` to `input: 'src/main.ts'`

Add `typescript()` to list of plugins
Add `preprocess: preprocess()` to Svelte plugin options.

#### 5. Add tsconfig.json
```json
{
    "include": ["src/**/*"],
    "exclude": ["node_modules/*"],
    "compilerOptions": {
        "target": "es2017",
        "types": ["svelte"],
        "moduleResolution": "node"
    }
}
```

#### 6. Add svelte.config.js
```js
const { preprocess } = require('@pyoner/svelte-ts-preprocess');

module.exports = {
preprocess: preprocess(),
};
```

#### 7. Add prettierrc.js
```js
module.exports = {
    printWidth: 120,
    plugins: ['prettier-plugin-svelte'],
    svelteSortOrder: 'styles-scripts-markup',
    svelteStrictMode: false,
    svelteBracketNewLine: true,
};
```