---
sidebar_position: 4
---

# NestJS

## Cài đặt dev dependencies

```bash
npm install -D eslint prettier eslint-config-prettier eslint-plugin-prettier @typescript-eslint/parser @typescript-eslint/eslint-plugin eslint-plugin-import eslint-import-resolver-typescript eslint-plugin-simple-import-sort lint-staged
```

## File `.eslintrc.js`

```js title=".eslintrc.js"
module.exports = {
  parser: "@typescript-eslint/parser",
  parserOptions: {
    project: "tsconfig.json",
    tsconfigRootDir: __dirname,
    sourceType: "module",
  },
  plugins: ["simple-import-sort"],
  extends: [
    "eslint:recommended",
    "plugin:@typescript-eslint/recommended",
    "prettier",
    "plugin:import/recommended",
    "plugin:import/typescript",
    "plugin:prettier/recommended",
  ],
  root: true,
  settings: {
    "import/resolver": {
      node: {
        paths: ["./src"],
        extensions: [".js", ".ts"],
      },
      typescript: {
        project: "./tsconfig.json",
      },
    },
  },
  env: {
    node: true,
    jest: true,
  },
  rules: {
    "prettier/prettier": "error",
    "no-unused-vars": "off",
    "no-empty": "off",
    "no-console": "off",
    "@typescript-eslint/no-unused-vars": "off",
    "@typescript-eslint/consistent-type-exports": "error",
    "@typescript-eslint/no-explicit-any": "off",
    "@typescript-eslint/no-empty-object-type": "off",
    "@typescript-eslint/no-restricted-imports": [
      "error",
      { patterns: ["../*"] },
    ],
    "simple-import-sort/imports": [
      "error",
      {
        groups: [["^(?!\\.)"], ["^\\u0000", "^\\.", "^src/"]],
      },
    ],
    "simple-import-sort/exports": "error",
    "import/newline-after-import": "error",
  },
};
```

## File `.eslintignore`

:::info

- ESLint sẽ áp dụng đối với tất cả các file trong dự án, ngoại trừ các file, folder ta định nghĩa trong file **.eslintignore**

:::

```plaintext title=".eslintignore"
node_modules
package-lock.json
.eslintrc.js
dist
build
```

## File `.prettierrc.json`

```json title=".prettierrc.json"
{
  "printWidth": 80,
  "tabWidth": 2,
  "useTabs": false,
  "semi": true,
  "singleQuote": true,
  "quoteProps": "as-needed",
  "jsxSingleQuote": false,
  "trailingComma": "none",
  "bracketSameLine": false,
  "arrowParens": "always",
  "insertPragma": false,
  "proseWrap": "preserve",
  "htmlWhitespaceSensitivity": "css",
  "embeddedLanguageFormatting": "auto",
  "bracketSpacing": true,
  "requirePragma": false,
  "endOfLine": "auto"
}
```

## File `.prettierignore`

```plaintext title=".prettierignore"
node_modules
build
dist
package-lock.json
```

## Cập nhật script cho lint-staged trong package.json

```json title="package.json"
{
  "name": "MyProject",
  "version": "0.1.0",
  "private": true,
  "scripts": {
    "lint": "eslint --fix .",
    "format": "prettier --write .",
    "ts-check": "tsc --noEmit",
    "prepare": "husky install"
  },
  "lint-staged": {
    "*.{ts,js}": ["prettier --write .", "eslint --fix .", "git add ."]
  }
}
```

## Cài đặt Husky

:::caution

Lưu ý: trước khi cài đặt, đảm bảo rằng dự án của bạn đã được liên kết với một repository trên Github hoặc Gitlab

:::

- Mở Git bash và gõ lệnh sau:

```bash
npx husky-init && npm install
```

- Trong file **pre-commit** thuộc thư mục **.husky** được tạo ra:

```text title=".husky/pre-commit"
#!/usr/bin/env sh
. "$(dirname -- "$0")/_/husky.sh"

npx lint-staged
```