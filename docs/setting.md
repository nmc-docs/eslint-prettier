---
sidebar_position: 2
---

# Cài đặt

## Cài đặt các devDependencies cần thiết:

```bash
npm i -D eslint prettier @typescript-eslint/parser @typescript-eslint/eslint-plugin eslint-config-prettier eslint-plugin-prettier eslint-plugin-import eslint-import-resolver-typescript eslint-plugin-simple-import-sort lint-staged
```

- Nếu sử dụng React thì cài thêm các thư viện sau:

```bash
npm i -D eslint-plugin-react eslint-plugin-react-hooks eslint-plugin-jsx-a11y
```

## Tạo file `.eslintrc.json`

```json title=".eslintrc.json"
{
  "root": true,
  "parser": "@typescript-eslint/parser",
  "extends": [
    "eslint:recommended",
    "plugin:@typescript-eslint/recommended",
    "plugin:react/recommended", // For React
    "plugin:react/jsx-runtime", // For React
    "plugin:react-hooks/recommended", // For React
    "plugin:jsx-a11y/recommended", // For React
    "plugin:import/recommended",
    "plugin:import/typescript",
    "plugin:prettier/recommended"
  ],
  "parserOptions": {
    "ecmaVersion": "latest",
    "sourceType": "module",
    "ecmaFeatures": {
      "jsx": true // For React
    },
    "project": "./tsconfig.json"
  },
  "plugins": ["prettier", "simple-import-sort"],
  "settings": {
    "react": {
      "version": "detect" // For React
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
    "node": true
  },
  "rules": {
    "no-unreachable": "error",
    "no-unused-vars": "off",
    "require-await": "error",
    "no-promise-executor-return": "error",
    "curly": "error",
    "camelcase": "error",
    "default-case": "error",
    "default-case-last": "error",
    "default-param-last": "error",
    "eqeqeq": "error",
    "no-else-return": "error",
    "no-empty": "off",
    "no-lonely-if": "error",
    "no-unneeded-ternary": "error",
    "no-useless-rename": "error",
    "no-throw-literal": "error",
    "no-useless-return": "error",
    "object-shorthand": "error",
    "prefer-template": "error",
    "prettier/prettier": "warn",
    "@typescript-eslint/no-restricted-imports": [
      "error",
      { "patterns": ["../*"] }
    ],
    "@typescript-eslint/await-thenable": "error",
    "@typescript-eslint/consistent-type-exports": "error",
    "@typescript-eslint/method-signature-style": "error",
    "@typescript-eslint/no-duplicate-type-constituents": "error",
    "@typescript-eslint/no-explicit-any": "off",
    "@typescript-eslint/no-floating-promises": [
      "error",
      { "ignoreIIFE": true }
    ],
    "@typescript-eslint/no-inferrable-types": "off",
    "@typescript-eslint/no-require-imports": "error",
    "@typescript-eslint/no-unnecessary-boolean-literal-compare": "error",
    "@typescript-eslint/no-unnecessary-condition": "error",
    "@typescript-eslint/no-unnecessary-type-assertion": "error",
    "@typescript-eslint/no-unnecessary-type-constraint": "error",
    "@typescript-eslint/no-unnecessary-type-arguments": "error",
    "@typescript-eslint/no-useless-empty-export": "error",
    "@typescript-eslint/prefer-for-of": "error",
    "@typescript-eslint/prefer-function-type": "error",
    "@typescript-eslint/prefer-optional-chain": "error",
    "@typescript-eslint/prefer-reduce-type-parameter": "error",
    "@typescript-eslint/prefer-string-starts-ends-with": "error",
    "@typescript-eslint/require-array-sort-compare": [
      "error",
      { "ignoreStringArrays": true }
    ],
    "@typescript-eslint/restrict-plus-operands": "error",
    "@typescript-eslint/switch-exhaustiveness-check": "error",
    "@typescript-eslint/no-unused-vars": [
      "warn",
      {
        "argsIgnorePattern": "^_"
      }
    ],
    "import/extensions": "off",
    "import/export": "error",
    "import/no-empty-named-blocks": "error",
    "import/no-mutable-exports": "error",
    "import/no-named-as-default": "error",
    "import/consistent-type-specifier-style": "error",
    "import/first": "error",
    "import/newline-after-import": "error",
    "import/no-anonymous-default-export": "error",
    "simple-import-sort/imports": [
      "error",
      {
        "groups": [["^(?!\\.)"], ["^\\u0000", "^\\.", "^src/"]]
      }
    ],
    "simple-import-sort/exports": "error",
    // For React
    "react/jsx-boolean-value": ["error", "never"],
    "react/function-component-definition": [
      "error",
      { "namedComponents": "arrow-function" }
    ],
    "react/jsx-filename-extension": ["error", { "extensions": [".tsx"] }],
    "react/jsx-no-target-blank": "error",
    "react/jsx-pascal-case": "error",
    "react/react-in-jsx-scope": "off",
    "jsx-a11y/label-has-associated-control": "error",
    "jsx-a11y/media-has-caption": "off"
  }
}
```

## Tạo file `.prettierrc.json`

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

## Tạo file `.eslintignore`

- Không áp dụng các rules của ESLint đối với các file / folder này:

```ignore title=".eslintignore"
/node_modules
/build
/dist
package-lock.json
vite.config.ts
tailwind.config.js
postcss.config.js
webpack.config.js
```

## Tạo file `.prettierignore`

- Không định dạng format theo Prettier đối với những file/ folder này:

```ignore title=".prettierignore"
/node_modules
/build
/dist
package-lock.json
```

## Cập nhật script cho lint-staged trong package.json

```json title="package.json"
// Lưu ý viết dòng này cùng cấp với "scripts"
"lint-staged": {
  "*.{ts,tsx,js}": [
    "prettier --write .",
    "eslint --fix .",
    "eslint .",
    "git add ."
  ]
},
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

```text title=".husky/pre-commit"
#!/usr/bin/env sh
. "$(dirname -- "$0")/_/husky.sh"

npx lint-staged
```

## Tạo file `.editorconfig`

- File này là một tệp cấu hình dùng để định dạng mã nguồn trong các trình soạn thảo code. Nó là một tệp cấu hình được sử dụng để đồng nhất các cài đặt về định dạng mã nguồn như thụt đầu dòng, dấu tab hoặc dấu cách, độ rộng của tab, cách xuống dòng và nhiều thiết lập khác giữa các thành viên trong một dự án phát triển.

```.editorconfig title=".editorconfig"
root = true

[*]
charset = utf-8
indent_style = space
indent_size = 2
trim_trailing_whitespace = true
```

## Thiết lập setting trong file `setting.json`

- Mở file `setting.json` và bổ sung những cài đặt sau đây (nếu chưa có):

```json title="setting.json"
{
  "workbench.iconTheme": "material-icon-theme",
  "debug.terminal.clearBeforeReusing": true,
  "liveServer.settings.donotShowInfoMsg": true,
  "editor.linkedEditing": true,
  "workbench.editor.wrapTabs": true,
  "workbench.editor.untitled.hint": "hidden",
  "editor.wordWrap": "on",
  "terminal.integrated.enableMultiLinePasteWarning": false,
  "git.confirmSync": false,
  "git.enableSmartCommit": true,
  "tabnine.experimentalAutoImports": true,
  "editor.codeActionsOnSave": {
    "source.fixAll": true
  },
  "scss.showErrors": true,
  "javascript.updateImportsOnFileMove.enabled": "always",
  "editor.fontFamily": "JetBrains Mono",
  "git.openRepositoryInParentFolders": "always",
  "typescript.updateImportsOnFileMove.enabled": "always",
  "eslint.format.enable": true,
  "editor.formatOnSave": true,
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  "editor.fontSize": 15,
  "editor.tabSize": 2,
  "workbench.colorTheme": "Default Dark+",
  "terminal.integrated.defaultProfile.windows": "Git Bash",
  "editor.inlineSuggest.enabled": true,
  "workbench.editorAssociations": {
    "*.svg": "default",
    // "*.md": "default",
    "*.png": "imagePreview.previewEditor"
  },
  "svg.preview.autoShow": true,
  "svg.preview.mode": "img"
}
```
