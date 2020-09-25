# React Template

This is a template for React with Typescript, ESLint, Prettier and VSCode configured

# References

- [https://medium.com/@feralamillo/create-react-app-typescript-eslint-and-prettier-699277b0b913](https://medium.com/@feralamillo/create-react-app-typescript-eslint-and-prettier-699277b0b913)
- [https://medium.com/@smagluf/for-anyone-having-issues-regarding-the-eslint-version-its-due-to-the-fact-that-the-2d2ac1ebfb31](https://medium.com/@smagluf/for-anyone-having-issues-regarding-the-eslint-version-its-due-to-the-fact-that-the-2d2ac1ebfb31)
- [https://medium.com/@brygrill/create-react-app-with-typescript-eslint-prettier-and-github-actions-f3ce6a571c97](https://medium.com/@brygrill/create-react-app-with-typescript-eslint-prettier-and-github-actions-f3ce6a571c97)
- https://stackoverflow.com/questions/63818415/react-was-used-before-it-was-defined

# Steps to reproduce

1. create app

   ```bash
   npx create-react-app <app> --typescript
   ```

1. install plugins

   ```bash
   npm i --save-dev eslint-plugin-import eslint-plugin-jsx-a11y eslint-plugin-react-hooks eslint-plugin-react
   npm i --save-dev @typescript-eslint/eslint-plugin@4.0.1 @typescript-eslint/parser@4.0.1 eslint-config-airbnb-typescript@6.3.2
   ```

1. install prettier

   ```bash
   npm i --save-dev prettier eslint-config-prettier eslint-plugin-prettier
   ```

1. create `eslintrc.yaml`

   - code

     ```yaml
     ---
     env:
       browser: true
       es2020: true
     extends:
       - airbnb
       - airbnb/hooks
       - plugin:@typescript-eslint/recommended
       - plugin:react/recommended
       - plugin:import/errors
       - plugin:import/warnings
       - plugin:import/typescript
       # always put prettier last
       - prettier/@typescript-eslint # Uses eslint-config-prettier to disable ESLint rules from @typescript-eslint/eslint-plugin that would conflict with prettier
       - plugin:prettier/recommended # Enables eslint-plugin-prettier and eslint-config-prettier. This will display prettier errors as ESLint errors. Make sure this is always the last configuration in the extends array.

       # doesn't work instead of plugin:prettier/recommended
       # - prettier

     globals:
       Atomics: readonly
       SharedArrayBuffer: readonly
     parser: "@typescript-eslint/parser"
     parserOptions:
       ecmaFeatures:
         jsx: true
       ecmaVersion: 2020
       sourceType: module
     plugins:
       - react
       - "@typescript-eslint"
       - prettier
     rules:
       # rule's settings
       # --------------------------------
       # "off" or 0 - turn the rule off
       # "warn" or 1 - turn the rule on as a warning (doesn't affect exit code)
       # "error" or 2 - turn the rule on as an error (exit code is 1 when triggered)
       #
       # additional rule options
       # --------------------------------
       # quotes: ["error", "double"]

       # use prettierrc.yaml
       # doesn't work too well here?
       # prettier/prettier:
       # - 'error' # ?
       # - tabWidth: 2
       # - singleQuote: true

       react/destructuring-assignment: [error, never]

       react/jsx-filename-extension: "off"
       import/extensions: "off"
       import/prefer-default-export: "off"
       react/jsx-one-expression-per-line: "off"

       # Don't allow unused variables
       no-unused-vars: "error"

       # https://github.com/airbnb/javascript/pull/2136
       # https://github.com/jsx-eslint/eslint-plugin-jsx-a11y/issues/632
       jsx-a11y/label-has-associated-control:
         - error
         - labelComponents: []
           labelAttributes: []
           controlComponents: []
           assert: either
           depth: 25

       # Allow untyped functions
       # must be quoted
       "@typescript-eslint/explicit-module-boundary-types": off

       # Require naming react components
       react/display-name: "error"

       # NextJs specific fix: suppress errors for missing 'import React' in files for nextjs
       react/react-in-jsx-scope: "off"

     settings:
       import/resolver:
         node:
           extensions:
             - ".js"
             - ".jsx"
             - ".ts"
             - ".tsx"
             - ".d.ts"
     ```

1. create `prettierrc.yaml`

   ```yaml
   semi: false
   trailingComma: "all"
   singleQuote: false
   printWidth: 120
   tabWidth: 4
   ```

1. install eslint and prettier extension for vscode
1. vscode settings for auto fixes `.vscode/settings.json`

   ```bash
   {
     "editor.codeActionsOnSave": {
       "source.fixAll.eslint": true
     },
     "editor.formatOnSave": true
   }
   ```

1. create `.eslintignore`

   ```bash
   # don't ever lint node_modules
   node_modules
   ```

1. edit `package.json`

   ```yaml
   "scripts": { "lint": "eslint '*/**/*.{js,ts,tsx}' --quiet --fix" }
   ```
