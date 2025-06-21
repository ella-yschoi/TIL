# TypeScript Settings

## 1. TypeScript 프로젝트 환경 구성

### 1. 프로젝트 폴더 생성

```shell
mkdir (폴더명)
cd (폴더명)
```

### 2. 프로젝트 폴더 안에서 초기화

```shell
npm init -y
```

### 3. TypeScript 설치

```shell
npm install typescript --save-dev
```

### 4. 프로젝트 루트 디렉토리에 .json 파일 생성 후 붙여넣기

```json
//tsconfig.json
//compilerOptions 내의 속성은 커스텀 가능
{
  "compilerOptions": {
    "target": "es6",
    "module": "commonjs",
    "sourceMap": true,
    "outDir": "./dist"
  },
  "include": [
    "src/**/*"
  ]
}
```

### 5. src 폴더 안에 .ts 파일을 만들어 TypeScript 코드 작성

<br/>

## 2. TypeScript ESLint와 Prettier 설정하기

### 1. ESLint 설치 후, settings.json에 아래 설정 적용

```json
{
  // ... 
  "editor.codeActionsOnSave": {
      "source.fixAll.eslint": true
  },
  "eslint.alwaysShowStatus": true,
  "eslint.workingDirectories": [
      {"mode": "auto"}
  ],
  "eslint.validate": [
      "javascript",
      "typescript"
  ],
}

```

### 2. VSCode 에디터 설정 중 'format on save' 설정 해제

### 3. Prettier 설치 후, 프리셋과 라이브러리 설치

```shell
npm i -D @babel/core @babel/preset-env @babel/preset-typescript @typescript-eslint/eslint-plugin @typescript-eslint/parser eslint prettier eslint-plugin-prettier
```

### 4. 프로젝트 폴더 밑에 .eslintrc.js 파일을 만들어 아래 내용 붙여 넣기

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
