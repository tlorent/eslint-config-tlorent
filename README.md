# eslint-config-tlorent

To install the peer dependencies (ESLint & TypeScript) and the necessary dependencies (ESLint plugins):

`npx install-peerdeps --dev eslint-config-tlorent`

### extends

Create a new file **eslint.rc** in the root of your project (useful if you plan to add your own rules, otherwise package.json can become a mess) or add a new entry in **package.json** (if you are just extending this config):

**eslint.rc**

```json
{
    "extends": "tlorent",
    "rules": {
        "yourOwnRule": "rule",
        "etc": "etc"
    }
}
```

**package.json** (if you used Create-React-App or Gatsby, there might already be an "eslintConfig" entry. Remove and replace).

```json
{
    "eslintConfig": {
        "extends": "tlorent"
    }
}
```

### Commit hooks

> Add commit hooks to prevent 💩💩💩 from slipping into your codebase. -- [lint-staged](https://github.com/okonet/lint-staged)

`npx mrm lint-staged`

After running above command, this is a possible config for commit hooks:

```json
"scripts": {
    "typecheck": "tsc --project . --noEmit"
},
"husky": {
    "hooks": {
      "pre-commit": "npm run typecheck && lint-staged"
    }
},
"lint-staged": {
    "*.{js,ts}?(x)": [
        "eslint --fix",
        "prettier --write"
    ]
}
```

### TSConfig

Add a **tsconfig.jon** file in the root of your project. You can do this with `npx tsc --init` and then modify the generated config file or use this example config:

```json
{
    "compilerOptions": {
        /* Visit https://aka.ms/tsconfig.json to read more about this file */

        "target": "es5",
        "module": "commonjs",
        "jsx": "react",
        "sourceMap": true,
        "outDir": "./lib",
        "noEmit": true,
        "strict": true,
        "noImplicitAny": true,
        "strictNullChecks": true,
        "noUnusedParameters": true,
        "noImplicitReturns": true,
        "esModuleInterop": true,
        "skipLibCheck": true,
        "forceConsistentCasingInFileNames": true
    },
    "include": ["src"]
}
```
