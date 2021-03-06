# `@xpring-eng/eslint-config-base`

[![npm version](https://img.shields.io/npm/v/@xpring-eng/eslint-config-base.svg)](https://www.npmjs.com/package/@xpring-eng/eslint-config-base)
[![Downloads/month](https://img.shields.io/npm/dm/@xpring-eng/eslint-config-base.svg)](http://www.npmtrends.com/@xpring-eng/eslint-config-base)

A super-strict TypeScript linting configuration for enforcing best practices.

### Installation

First, install the needed development dependencies:

```sh
# Ensure TypeScript and the TS ESLint parser are installed
npm install --save-dev typescript @typescript-eslint/parser
# Ensure ESLint & Prettier are installed
npm install --save-dev eslint prettier
# Install plugins used by @xpring-eng/eslint-config-base
npm install --save-dev @typescript-eslint/eslint-plugin eslint-plugin-import eslint-plugin-prettier eslint-plugin-jsdoc eslint-plugin-tsdoc eslint-plugin-array-func eslint-plugin-eslint-comments eslint-plugin-node

# Install the Xpring ESLint config
npm install --save-dev @xpring-eng/eslint-config-base
```

### Usage

Then, configure your ESLint to use the Xpring configuration. An example ESLint configuration is provided below:

```js
module.exports = {
  root: true,

  // Make ESLint compatible with TypeScript
  parser: '@typescript-eslint/parser',
  parserOptions: {
    // Enable linting rules with type information from our tsconfig
    tsconfigRootDir: __dirname,
    project: ['./tsconfig.json'],

    // Allow the use of imports / ES modules
    sourceType: 'module',

    ecmaFeatures: {
      // Enable global strict mode
      impliedStrict: true,
    },
  },

  // Specify global variables that are predefined
  env: {
    node: true, // Enable node global variables & Node.js scoping
    es2020: true, // Add all ECMAScript 2020 globals and automatically set the ecmaVersion parser option to ES2020
  },

  plugins: [],
  // extends: ['@xpring-eng/eslint-config-base'],
  extends: ['@xpring-eng/eslint-config-base/loose'],
  rules: {},
  overrides: [],
}
```

### Recommended Configs

We provide two different configurations.

The stricter configuration is `@xpring-eng/eslint-config-base`, which is configured to provide best practices for a mature TS project.

However, while transitioning to this linting configuration, it is useful to have a less strict configuration to work with.
The looser configuration is `@xpring-eng/eslint-config-base/loose`.

#### Loose Config

The looser configuration differs in the following ways:

- Longer line length limitation for functions
- More import statements allowed per file
- More parameters allowed per function
- The very strict `no-unsafe-*` rules from `@typescript-eslint` are disabled
- Type assertions are allowed
