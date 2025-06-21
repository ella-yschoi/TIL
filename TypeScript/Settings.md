# TypeScript Settings

## 1. TypeScript Project Environment Setup

### 1. Create Project Folder

```shell
mkdir (folder_name)
cd (folder_name)
```

### 2. Initialize Inside Project Folder

```shell
npm init -y
```

### 3. Install TypeScript

```shell
npm install typescript --save-dev
```

### 4. Create .json File in Project Root Directory and Paste

```json
//tsconfig.json
//Properties within compilerOptions can be customized
{
  "compilerOptions": {
    "target": "es6",
    "module": "commonjs",
    "sourceMap": true,
    "outDir": "./dist"
  },
  "include": ["src/**/*"]
}
```

### 5. Create .ts File Inside src Folder and Write TypeScript Code

<br/>

## 2. Setting Up TypeScript ESLint and Prettier

### 1. Install ESLint, Then Apply Settings Below to settings.json

```json
{
  // ...
  "editor.codeActionsOnSave": {
    "source.fixAll.eslint": true
  },
  "eslint.alwaysShowStatus": true,
  "eslint.workingDirectories": [{ "mode": "auto" }],
  "eslint.validate": ["javascript", "typescript"]
}
```

### 2. Disable 'format on save' Setting in VSCode Editor Settings

### 3. Install Prettier, Then Install Presets and Libraries

```shell
npm i -D @babel/core @babel/preset-env @babel/preset-typescript @typescript-eslint/eslint-plugin @typescript-eslint/parser eslint prettier eslint-plugin-prettier
```

### 4. Create .eslintrc.js File Under Project Folder and Paste Content Below

```javascript
module.exports = {
  root: true,
  env: {
    browser: true,
    node: true,
    jest: true,
  },
  extends: [
    'plugin:@typescript-eslint/eslint-recommended',
    'plugin:@typescript-eslint/recommended',
  ],
  plugins: ['prettier', '@typescript-eslint'],
  rules: {
    'prettier/prettier': [
      'error',
      {
        singleQuote: true,
        tabWidth: 2,
        printWidth: 80,
        bracketSpacing: true,
        arrowParens: 'avoid',
      },
    ],
    '@typescript-eslint/no-explicit-any': 'off',
    '@typescript-eslint/explicit-function-return-type': 'off',
    'prefer-const': 'off',
  },
  parserOptions: {
    parser: '@typescript-eslint/parser',
  },
};
```
