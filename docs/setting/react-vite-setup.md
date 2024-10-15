---
sidebar_position: 2
---

# React Vite

## Cài đặt dev dependencies

```bash
npm install -D eslint@8.57.1 prettier eslint-config-prettier eslint-plugin-prettier @typescript-eslint/parser @typescript-eslint/eslint-plugin eslint-plugin-jsx-a11y eslint-plugin-react eslint-plugin-react-hooks eslint-plugin-import eslint-import-resolver-typescript eslint-plugin-simple-import-sort eslint-plugin-unused-imports lint-staged
```

:::note

- Nếu sử dụng TailwindCSS thì cài thêm:

```bash
npm install -D eslint-plugin-tailwindcss
```

:::

## File `.eslintrc.json`

```json title=".eslintrc.json"
{
  "root": true,
  "parser": "@typescript-eslint/parser",
  "extends": [
    "eslint:recommended",
    "plugin:@typescript-eslint/recommended",
    "plugin:react/recommended",
    "plugin:react/jsx-runtime",
    "plugin:react-hooks/recommended",
    "plugin:tailwindcss/recommended", // Nếu sử dụng TailwindCSS thì thêm dòng này
    "plugin:jsx-a11y/recommended",
    "prettier",
    "plugin:import/recommended",
    "plugin:import/typescript",
    "plugin:prettier/recommended"
  ],
  "parserOptions": {
    "ecmaVersion": "latest",
    "sourceType": "module",
    "ecmaFeatures": {
      "jsx": true
    },
    "project": "./tsconfig.app.json"
  },
  "settings": {
    "react": {
      "version": "detect"
    },
    "import/resolver": {
      "node": {
        "paths": ["./src"],
        "extensions": [".js", ".jsx", ".ts", ".tsx", ".css", ".scss", ".json"]
      },
      "typescript": {
        "project": "./tsconfig.app.json"
      }
    }
  },
  "env": {
    "node": true,
    "browser": true,
    "es6": true
  },
  "plugins": ["simple-import-sort", "unused-imports"],
  "rules": {
    "prettier/prettier": "error",
    "no-unused-vars": "off",
    "no-empty": "off",
    "no-console": "off",
    "@typescript-eslint/no-unused-vars": [
      "error",
      {
        "args": "all",
        "argsIgnorePattern": "^_",
        "caughtErrors": "all",
        "caughtErrorsIgnorePattern": "^_",
        "destructuredArrayIgnorePattern": "^_",
        "varsIgnorePattern": "^_",
        "ignoreRestSiblings": true
      }
    ],
    "@typescript-eslint/consistent-type-exports": "error",
    "@typescript-eslint/no-explicit-any": "off",
    "@typescript-eslint/no-empty-object-type": "off",
    "@typescript-eslint/no-restricted-imports": [
      "error",
      { "patterns": ["../*"] }
    ],
    "simple-import-sort/imports": [
      "error",
      {
        "groups": [["^(?!\\.)"], ["^\\u0000", "^\\.", "^src/"]]
      }
    ],
    "simple-import-sort/exports": "error",
    "import/newline-after-import": "error",
    "unused-imports/no-unused-imports": "error"
  }
}
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

## File `.lintstagedrc.json`

```json title=".lintstagedrc.json"
{
  "*": ["prettier --write .", "git add ."],
  "src/**/*.{ts,tsx}": ["eslint --fix --max-warnings=0", "git add ."]
}
```

## Cập nhật script trong package.json

```json title="package.json"
{
  "name": "MyProject",
  "version": "0.1.0",
  "private": true,
  "scripts": {
    "lint": "eslint \"src/**/*.{ts,tsx}\" --fix",
    "format": "prettier --write .",
    "ts-check": "tsc --noEmit",
    "prepare": "husky install"
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
