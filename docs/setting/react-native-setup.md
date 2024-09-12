---
sidebar_position: 3
---

# React Native

## Cài đặt dev dependencies

```bash
npm install -D eslint prettier eslint-config-prettier eslint-plugin-prettier @typescript-eslint/parser @typescript-eslint/eslint-plugin eslint-plugin-jsx-a11y eslint-plugin-react eslint-plugin-react-hooks eslint-plugin-import eslint-import-resolver-typescript eslint-plugin-simple-import-sort lint-staged
```

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
    "project": "./tsconfig.json"
  },
  "settings": {
    "react": {
      "version": "detect"
    },
    "import/resolver": {
      "node": {
        "paths": ["./src"],
        "extensions": [".ts", ".tsx", ".js"]
      },
      "typescript": {
        "project": "./tsconfig.json"
      }
    },
    "import/ignore": ["react-native"]
  },
  "env": {
    "node": true,
    "browser": true,
    "es6": true
  },
  "plugins": ["simple-import-sort"],
  "rules": {
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
      { "patterns": ["../*"] }
    ],
    "simple-import-sort/imports": [
      "error",
      {
        "groups": [["^(?!\\.)"], ["^\\u0000", "^\\.", "^@src/"]]
      }
    ],
    "simple-import-sort/exports": "error",
    "import/newline-after-import": "error"
  }
}
```

## File `.eslintignore`

:::info

- ESLint sẽ áp dụng đối với tất cả các file trong dự án, ngoại trừ các file, folder ta định nghĩa trong file **.eslintignore**

:::

```plaintext title=".eslintignore"
node_modules
package-lock.json
tailwind.config.js
babel.config.js
metro.config.js
tailwind.js
jest.config.js
metro.config.js
react-native.config.js
babel.config.js
__tests__
.bundle
.idea
android
ios
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
    "*.{ts,tsx,js}": ["prettier --write .", "eslint --fix .", "git add ."]
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
