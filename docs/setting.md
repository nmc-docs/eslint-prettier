---
sidebar_position: 2
---

# Cài đặt

## Cài đặt các devDependencies cần thiết:

```bash
npm install -D eslint prettier eslint-config-prettier eslint-plugin-prettier @typescript-eslint/parser @typescript-eslint/eslint-plugin eslint-plugin-import eslint-import-resolver-typescript eslint-plugin-simple-import-sort lint-staged
```

- Nếu sử dụng React thì cài thêm các thư viện sau:

```bash
npm install -D eslint-config-next eslint-plugin-jsx-a11y eslint-plugin-react eslint-plugin-react-hooks eslint-plugin-tailwindcss
```

## Tạo file `.eslintrc.json`

### Cho dự án Nextjs:

```json
{
  "root": true,
  "parser": "@typescript-eslint/parser",
  "extends": [
    "next/core-web-vitals",
    "eslint:recommended",
    "plugin:@typescript-eslint/recommended",
    "plugin:@typescript-eslint/recommended-type-checked",
    "plugin:@typescript-eslint/strict",
    "plugin:@typescript-eslint/strict-type-checked",
    "plugin:react/recommended",
    "plugin:react/jsx-runtime",
    "plugin:react-hooks/recommended",
    "plugin:jsx-a11y/recommended",
    "plugin:tailwindcss/recommended",
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
        "extensions": [".js", ".jsx", ".ts", ".tsx", ".css", ".scss"]
      },
      "typescript": {
        "project": "./tsconfig.json"
      }
    }
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
    "@next/next/no-async-client-component": "error"
  }
}
```

### Cho dự án khác

```json
{
  "root": true,
  "parser": "@typescript-eslint/parser",
  "extends": [
    "eslint:recommended",
    "plugin:@typescript-eslint/recommended",
    "plugin:@typescript-eslint/recommended-type-checked",
    "plugin:@typescript-eslint/strict",
    "plugin:@typescript-eslint/strict-type-checked",
    "prettier",
    "plugin:import/recommended",
    "plugin:import/typescript",
    "plugin:prettier/recommended"
  ],
  "parserOptions": {
    "ecmaVersion": "latest",
    "sourceType": "module",
    "project": "./tsconfig.json"
  },
  "settings": {
    "import/resolver": {
      "node": {
        "paths": ["./src"],
        "extensions": [".js", ".ts"]
      },
      "typescript": {
        "project": "./tsconfig.json"
      }
    }
  },
  "env": {
    "node": true,
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
    "import/newline-after-import": "error"
  }
}
```

## Tạo file `.prettierrc.json`

```json
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

## Tạo file `.eslintignore`

- Không áp dụng các rules của ESLint đối với các file / folder này:

```ignore
node_modules
build
dist
.next
.idea
package-lock.json
tailwind.config.ts
postcss.config.js
next.config.js
```

## Tạo file `.prettierignore`

- Không định dạng format theo Prettier đối với những file/ folder này:

```ignore
node_modules
build
dist
.next
.idea
package-lock.json
```

## Cập nhật script cho lint-staged trong package.json

```json
{
  "name": "nextjs-learning",
  "version": "0.1.0",
  "private": true,
  "scripts": {
    "dev": "next dev",
    "build": "next build",
    "start": "next start",
    "lint": "next lint --fix",
    "prettier:fix": "prettier --write .",
    "eslint:fix": "eslint --fix .",
    "prepare": "husky install"
  },
  "lint-staged": {
    "*.{ts,tsx,js}": ["prettier --write .", "eslint --fix .", "git add ."]
  }
}
```

## Cài đặt Husky

:::caution

Lưu ý: trước khi cài đặt, đảm bảo rằng dự án của bạn đã được liên kết với một repository trên Github

:::

- Mở Git bash và gõ lệnh sau:

```bash
npx husky-init && npm install
```

- Trong file **pre-commit** thuộc thư mục **.husky** được tạo ra:

```text
#!/usr/bin/env sh
. "$(dirname -- "$0")/_/husky.sh"

npx lint-staged
```
