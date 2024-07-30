It's a repository to reproduce the issue happens in storybook typescript parsing.

The repo comes with a few simple steps:
1. `npx storybook@7 init` to init the storybook
2. install `cssnano`, `ts-node` and `typescript`
3. rename `./storybook/main.js` to `./storybook/main.ts` and add
```
import * as cssnano from 'cssnano';
console.log({ cssnano })
cssnano({});
```
to the top

5. create a `tsconfig.json` with the following content
```
{
  "compilerOptions": {
    "strict": true,
    "module": "commonjs",
    "target": "ES2019",
    "moduleResolution": "Node"
  },
}
```

6. Run `yarn storybook` and it crashes. `console.log` in 3 indicates typescript is ran with `allowSyntheticDefaultImports`, which is not part of my `tsconfig.json`
```
{
  cssnano: Function {
    default: [Function: cssnanoPlugin] { postcss: true },
    postcss: [Getter]
  }
}
```

7. Run `yarn ts-node .storybook/main.ts`, no errors and `console.log` in 3 gives:
```
{ cssnano: [Function: cssnanoPlugin] { postcss: true } }
```



