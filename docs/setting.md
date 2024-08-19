---
sidebar_position: 2
---
# Cài đặt

## Cài đặt các devDependencies cần thiết:

```bash
npm install -D eslint prettier eslint-config-prettier eslint-plugin-prettier @typescript-eslint/parser @typescript-eslint/eslint-plugin eslint-plugin-import eslint-import-resolver-typescript eslint-plugin-simple-import-sort lint-staged
```

- Nếu sử dụng React Native thì cài thêm các thư viện sau:

```bash
npm install -D eslint-plugin-jsx-a11y eslint-plugin-react eslint-plugin-react-hooks
```

- Nếu sử dụng NextJS thì cài thêm các thư viện sau:

```bash
npm install -D eslint-config-next eslint-plugin-react-hooks eslint-plugin-tailwindcss
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
    "plugin:react-hooks/recommended",
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
        "extensions": [".js", ".jsx", ".ts", ".tsx", ".css"]
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

### Cho dự án React Native

```json
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
        "extensions": [".ts", ".tsx"]
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

### Cho dự án NestJS (tên file là .eslintrc.js)

```js
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

:::info

- ESLint sẽ áp dụng đối với tất cả các file trong dự án, ngoại trừ các file, folder ta định nghĩa trong file **.eslintignore**

:::

```ignore
node_modules
package-lock.json
build
dist

/* For Nextjs project */
.next
.idea
tailwind.config.ts
postcss.config.js
next.config.js

/* For React Native project */
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
    "format": "prettier --write .",
    "ts-check": "tsc --noEmit",
    "prepare": "husky install"
  },
  "lint-staged": {
    "*.{ts,tsx,js,css,scss}": [
      "prettier --write .",
      "eslint --fix .",
      "git add ."
    ]
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

```text
#!/usr/bin/env sh
. "$(dirname -- "$0")/_/husky.sh"

npx lint-staged
```
