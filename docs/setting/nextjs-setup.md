---
sidebar_position: 1
---

# NextJS

## Cài đặt dev dependencies

```bash
npm install -D eslint eslint-config-next eslint-config-prettier @eslint/eslintrc @types/eslint__eslintrc @eslint/js eslint-config-next eslint-plugin-import eslint-import-resolver-typescript eslint-plugin-simple-import-sort eslint-plugin-unused-imports typescript-eslint prettier eslint-config-prettier eslint-plugin-prettier lint-staged
```

:::note

- Nếu dùng TailwindCSS, cài thêm:

```bash
npm install -D eslint-plugin-tailwindcss @types/eslint-plugin-tailwindcss prettier-plugin-tailwindcss
```

:::

## File `eslint.config.mjs`

```js title="eslint.config.mjs"
import { FlatCompat } from "@eslint/eslintrc";
import eslint from "@eslint/js";
import eslintPluginPrettierRecommended from "eslint-plugin-prettier/recommended";
import simpleImportSort from "eslint-plugin-simple-import-sort";
import tailwind from "eslint-plugin-tailwindcss";
import unusedImports from "eslint-plugin-unused-imports";
import { dirname } from "path";
import tseslint, { configs as tsEslintConfigs } from "typescript-eslint";
import { fileURLToPath } from "url";

const __filename = fileURLToPath(import.meta.url);
const __dirname = dirname(__filename);

const compat = new FlatCompat({
  baseDirectory: __dirname,
});

const eslintConfig = tseslint.config(
  { ignores: [".next/**/*", "node_modules/**/*"] },
  {
    files: ["src/**/*.{ts,tsx}", "eslint.config.mjs"],
    plugins: {
      "simple-import-sort": simpleImportSort,
      "unused-imports": unusedImports,
    },
    extends: [
      eslint.configs.recommended,
      eslintPluginPrettierRecommended,
      ...tsEslintConfigs.recommendedTypeChecked,
      ...tailwind.configs["flat/recommended"],
      ...compat.extends("next/core-web-vitals", "next/typescript"),
      ...compat.extends(
        "plugin:import/recommended",
        "plugin:import/typescript"
      ),
    ],
    languageOptions: {
      ecmaVersion: "latest",
      sourceType: "module",
      parserOptions: {
        projectService: true,
        tsconfigRootDir: import.meta.dirname,
      },
    },
    settings: {
      react: {
        version: "detect",
      },
      "import/resolver": {
        node: {
          paths: ["./src"],
          extensions: [".js", ".jsx", ".ts", ".tsx", ".css", ".scss", ".json"],
        },
        typescript: {
          project: "./tsconfig.json",
        },
      },
    },
    rules: {
      "no-unused-vars": "off",
      "no-empty": "off",
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
      "@next/next/no-async-client-component": "error",
    },
  }
  /* Cấu hình thêm ESLint, Plugin cho các file, thư mục khác. Cấu trúc như object bên trên */
);
export default eslintConfig;
```

:::note

- Đôi khi có những thư viện ESLint chưa hỗ trợ cấu hình với Flat Config mà chỉ tương thích với bản cũ (Legacy Config). Do đó, lớp `FlatCompat` được sinh ra và cung cấp cho ta các phương thức như `.extends()`, `.plugins()` để chuyển đổi chúng thành một cấu hình tương thích với Flat Config.

:::

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
/public
/.next
/.idea
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

:::info

- Các bước mà lint staged sẽ làm trước khi commit:
  - `prettier --write .`: Chạy format trên tất cả các file (ngoại trừ những file được cấu hình trong **.prettierignore**).
  - `npm run type-check`: Thực hiện kiểm tra xem có lỗi type hay không từ các file **.ts**, **.tsx** được `include` trong **tsconfig.json**
  - `eslint --fix --max-warnings=0 --no-warn-ignored`: Chạy ESLint kiểm tra các lỗi liên quan đến linter, bao gồm cả warning.
  - `git add .`: Nếu ESLint có thể tự fix được các lỗi liên quan đến linter, sau khi fix sẽ tự động thêm lại các file vào stage area trong Git.

:::

## Cập nhật script trong package.json

```json
{
  "name": "MyProject",
  "version": "0.1.0",
  "private": true,
  "scripts": {
    "dev": "next dev",
    "build": "next build",
    "start": "next start",
    "lint": "next lint --fix",
    "format": "prettier --write .",
    "type-check": "tsc --noEmit",
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

```text title=".husky\pre-commit"
#!/usr/bin/env sh
. "$(dirname -- "$0")/_/husky.sh"

npx lint-staged
```
