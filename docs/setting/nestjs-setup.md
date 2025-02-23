---
sidebar_position: 4
---

# NestJS

## Cài đặt dev dependencies

```bash
npm install -D eslint @eslint/eslintrc @types/eslint__eslintrc @eslint/js eslint-plugin-import eslint-import-resolver-typescript eslint-plugin-simple-import-sort eslint-plugin-unused-imports typescript-eslint prettier eslint-config-prettier eslint-plugin-prettier lint-staged globals
```

## File `eslint.config.mjs`

```js title="eslint.config.mjs"
// @ts-check
import { FlatCompat } from "@eslint/eslintrc";
import eslint from "@eslint/js";
import eslintPluginPrettierRecommended from "eslint-plugin-prettier/recommended";
import globals from "globals";
import { dirname } from "path";
import tseslint from "typescript-eslint";
import { fileURLToPath } from "url";
import unusedImports from "eslint-plugin-unused-imports";
import simpleImportSort from "eslint-plugin-simple-import-sort";

const __filename = fileURLToPath(import.meta.url);
const __dirname = dirname(__filename);

const compat = new FlatCompat({
  baseDirectory: __dirname,
});

export default tseslint.config(
  {
    ignores: [
      "node_modules/**/*",
      "dist/**/*",
      "coverage/**/*",
      "build/**/*",
      "eslint.config.mjs",
    ],
  },
  {
    files: ["src/**/*.ts"],
    plugins: {
      "simple-import-sort": simpleImportSort,
      "unused-imports": unusedImports,
    },
    extends: [
      eslint.configs.recommended,
      eslintPluginPrettierRecommended,
      ...tseslint.configs.recommendedTypeChecked,
      ...compat.extends(
        "plugin:import/recommended",
        "plugin:import/typescript"
      ),
    ],
    languageOptions: {
      globals: {
        ...globals.node,
        ...globals.jest,
      },
      ecmaVersion: 5,
      sourceType: "module",
      parserOptions: {
        projectService: true,
        tsconfigRootDir: import.meta.dirname,
      },
    },
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
    rules: {
      "prettier/prettier": "error",
      "no-unused-vars": "off",
      "no-empty": "off",
      "no-console": "off",
      "@typescript-eslint/no-unused-vars": [
        "error",
        {
          args: "all",
          argsIgnorePattern: "^_",
          caughtErrors: "all",
          caughtErrorsIgnorePattern: "^_",
          destructuredArrayIgnorePattern: "^_",
          varsIgnorePattern: "^_",
          ignoreRestSiblings: true,
        },
      ],
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
      "unused-imports/no-unused-imports": "error",
    },
  }
);
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
/node_modules
/build
/dist
package-lock.json
```

## File `.lintstagedrc.mjs`

```js title=".lintstagedrc.mjs"
export default {
  "*": () => [
    "prettier --write .",
    "npm run type-check",
    "eslint --fix --max-warnings=0 --no-warn-ignored",
    "git add .",
  ],
};
```

## Cập nhật script trong package.json

```json title="package.json"
{
  "name": "MyProject",
  "version": "0.1.0",
  "private": true,
  "scripts": {
    "dev": "nest start --watch",
    "lint": "eslint --fix",
    "type-check": "tsc --noEmit",
    "format": "prettier --write .",
    "build": "nest build",
    "start:prod": "node dist/main",
    "start:debug": "nest start --debug --watch",
    "start": "nest start",
    "test": "jest",
    "test:watch": "jest --watch",
    "test:cov": "jest --coverage",
    "test:debug": "node --inspect-brk -r tsconfig-paths/register -r ts-node/register node_modules/.bin/jest --runInBand",
    "test:e2e": "jest --config ./test/jest-e2e.json"
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
