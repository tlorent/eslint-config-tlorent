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

        /* Basic Options */
        "target": "es5" /* Specify ECMAScript target version: 'ES3' (default), 'ES5', 'ES2015', 'ES2016', 'ES2017', 'ES2018', 'ES2019', 'ES2020', or 'ESNEXT'. */,
        "module": "commonjs" /* Specify module code generation: 'none', 'commonjs', 'amd', 'system', 'umd', 'es2015', 'es2020', or 'ESNext'. */,
        "jsx": "react" /* Specify JSX code generation: 'preserve', 'react-native', or 'react'. */,
        "sourceMap": true /* Generates corresponding '.map' file. */,
        "outDir": "./lib" /* Redirect output structure to the directory. */,
        "noEmit": true /* Do not emit outputs. */,

        /* Strict Type-Checking Options */
        "strict": true /* Enable all strict type-checking options. */,
        "noImplicitAny": true /* Raise error on expressions and declarations with an implied 'any' type. */,
        "strictNullChecks": true /* Enable strict null checks. */,

        /* Additional Checks */
        "noUnusedParameters": true /* Report errors on unused parameters. */,
        "noImplicitReturns": true /* Report error when not all code paths in function return a value. */,

        /* Module Resolution Options */
        "esModuleInterop": true /* Enables emit interoperability between CommonJS and ES Modules via creation of namespace objects for all imports. Implies 'allowSyntheticDefaultImports'. */,

        /* Advanced Options */
        "skipLibCheck": true /* Skip type checking of declaration files. */,
        "forceConsistentCasingInFileNames": true /* Disallow inconsistently-cased references to the same file. */
    },
    "include": ["src"]
}
```
