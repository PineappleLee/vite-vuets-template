# Vue 3 + TypeScript + Vite

This template should help get you started developing with Vue 3 and TypeScript in Vite. The template uses Vue 3 `<script setup>` SFCs, check out the [script setup docs](https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup) to learn more.

## Recommended IDE Setup

- [VS Code](https://code.visualstudio.com/) + [Volar](https://marketplace.visualstudio.com/items?itemName=Vue.volar)

## Type Support For `.vue` Imports in TS

Since TypeScript cannot handle type information for `.vue` imports, they are shimmed to be a generic Vue component type by default. In most cases this is fine if you don't really care about component prop types outside of templates. However, if you wish to get actual prop types in `.vue` imports (for example to get props validation when using manual `h(...)` calls), you can enable Volar's Take Over mode by following these steps:

1. Run `Extensions: Show Built-in Extensions` from VS Code's command palette, look for `TypeScript and JavaScript Language Features`, then right click and select `Disable (Workspace)`. By default, Take Over mode will enable itself if the default TypeScript extension is disabled.
2. Reload the VS Code window by running `Developer: Reload Window` from the command palette.

You can learn more about Take Over mode [here](https://github.com/johnsoncodehk/volar/discussions/471).

## 使用步骤

### Step 1 准备工作

- ```shell
  pnpm create vite my-vuets-app --template vue-ts
  cd my-vuets-app
  git init
  pnpm install
  ```

- 在VScode中安装`ESLint`、`Stylelint`和`Prettier - Code formatter`插件

- 在.vscode目录下新建.settings.json文件

  ```json
  {
    "json.schemaDownload.enable": true,
    "emmet.triggerExpansionOnTab": true,
    "editor.tabSize": 2,
    "editor.defaultFormatter": "esbenp.prettier-vscode",
    "editor.formatOnSave": true,
    "editor.codeActionsOnSave": {
      "source.fixAll": true,
      "source.fixAll.eslint": true,
      "source.fixAll.stylelint": true
    },
    "typescript.tsdk": "node_modules/typescript/lib",
    "stylelint.validate": ["css", "less", "scss", "vue"],
    "eslint.format.enable": true
   }
  ```

- 在.gitignore文件里新增内容如下：

  ```
  !.vscode/settings.json
  ```

### Step 2 eslint校验与Prettier自动格式化

- ```sh
  pnpm install -D eslint eslint-plugin-vue eslint-config-prettier prettier eslint-config-standard eslint-plugin-import eslint-plugin-n eslint-plugin-promise
  
  pnpm install -D typescript @typescript-eslint/parser @typescript-eslint/eslint-plugin @types/node
  ```

- 新建`.eslintrc.cjs`文件

  ```js
  module.exports = {
    env: {
      browser: true,
      es2021: true,
      node:true
    },
    extends: [
      'eslint:recommended',
      'standard',
      'plugin:vue/vue3-strongly-recommended',
      'plugin:@typescript-eslint/recommended',
      'prettier',
    ],
    overrides: [],
    parser: 'vue-eslint-parser',
    parserOptions: {
      ecmaVersion: 'latest',
      sourceType: 'module',
      parser: '@typescript-eslint/parser',
      ecmaFeatures: {
        tsx: true,
        jsx: true,
      },
    },
    globals: {
      defineProps: 'readonly',
      defineEmits: 'readonly',
      defineExpose: 'readonly',
      withDefaults: 'readonly',
    },
    plugins: ['vue', '@typescript-eslint'],
    rules: {},
  }
  ```

- 新建`.prettierrc.cjs`文件

  ```js
  module.exports = {
  	// 一行最多 80 字符
  	printWidth: 80,
  	// 使用 2 个空格缩进
  	tabWidth: 2,
  	// 不适用缩进符，而是用空格
  	useTabs: false,
  	// 行尾需要有分号
  	semi:false,
  	// 使用单引号
  	singleQuote: true,
  	// 对象的 key 仅在必要时 用引号
  	quoteProps: 'as-needed',
  	// jsx不使用单引号，而使用双引号
  	jsxSingleQuote: false,
  	// 尾随逗号
  	trailingComma: 'es5',
  	// 大括号的首尾需要空格
  	bracketSpacing: true,
  	// 箭头函数，只有一个参数的时候，也需要括号
  	arrowParens: 'always',
  	// 每个文件格式化的范围是文件的全部内容
  	rangeStart: 0,
  	rangeEnd: Infinity,
  	// 不需要写文件开头的 @prettier
  	requirePragma: false,
  	// 不需要自动在文件开头插入 @prettier
  	insertPragma: false,
  	// 使用默认的折行标准
  	proseWrap: 'always',
  	// 根据显示样式决定 html 要不要折行
  	htmlWhitespaceSensitivity: 'css',
  	// 换行符使用lf
  	endOfLine: 'lf'
  }
  ```

- 新建`.eslintignore`文件

  ```
  *.sh
  node_modules
  *.md
  *.woff
  *.ttf
  .vscode
  .idea
  dist
  /public
  /docs
  .husky
  /bin
  .eslintrc.*js
  prettier.config.js
  /src/mock/*
  
  # Logs
  logs
  *.log
  npm-debug.log*
  yarn-debug.log*
  yarn-error.log*
  pnpm-debug.log*
  lerna-debug.log*
  
  .DS_Store
  dist-ssr
  *.local
  
  /cypress/videos/
  /cypress/screenshots/
  
  # Editor directories and files
  .vscode
  !.vscode/settings.json
  !.vscode/extensions.json
  .idea
  *.suo
  *.ntvs*
  *.njsproj
  *.sln
  *.sw?
  
  vite-env.d.ts
  components.d.ts
  ```

- 新建`.prettierignore`文件

  ```
  /dist/*
  .local
  .output.js
  /node_modules/**
  src/.DS_Store
  
  **/*.svg
  **/*.sh
  
  /public/*
  components.d.ts
  ```

###  Step 3 Stylelint校验

- ```sh
  pnpm install --save-dev stylelint stylelint-config-standard
  pnpm install -D less stylelint-config-recommended-vue stylelint-config-recommended-scss stylelint-config-recommended-less postcss postcss-html
  ```

- 新建`.stylelintrc.cjs`文件

  ```js
  module.exports = {
    extends: ['stylelint-config-standard', 'stylelint-config-recommended-vue'],
    overrides: [
      // 若项目中存在scss文件，添加以下配置
      {
        files: ['*.scss', '**/*.scss'],
        customSyntax: 'postcss-scss',
        extends: ['stylelint-config-recommended-scss'],
      },
      // 若项目中存在less文件，添加以下配置
      {
        files: ['*.less', '**/*.less'],
        customSyntax: 'postcss-less',
        extends: ['stylelint-config-recommended-less'],
      },
    ],
  }
  ```

- 新建`.stylelintignore`文件

  ```
  /dist/*
  /public/*
  node_modules
  ```

### Step 4 Husky、lint-staged、commitlint功能添加

- ```
  pnpm install lint-staged husky -D
  npx husky install
  npx husky add .husky/pre-commit "npx lint-staged"
  pnpm install @commitlint/config-conventional @commitlint/cli -D
  npx husky add .husky/commit-msg "npx --no -- commitlint --edit ${1}"
  ```

- 在package文件中添加内容

  ```json
  {
  	"scripts": {
      "lint": "eslint \"src/**/*.{js,vue,ts}\" --fix",
      "prettier-format": "prettier \"src/**/*.{vue,js,ts}\" --write",
      "lint:css": "stylelint **/*.{vue,css,sass,scss,less} --fix",
      "lint:all": "pnpm run lint && pnpm run prettier-format && pnpm run lint:css",
      "prepare": "husky install"
    },
    "lint-staged": {
      "src/**/*.{js,jsx,vue,ts,tsx}": [
        "eslint --fix",
        "prettier --write"
      ],
      "*.{vue,less,css,sass,scss}": [
        "stylelint --fix"
      ]
    },
  }
  ```

  

- 新建`commitlint.config.cjs`文件

  ```js
  module.exports = {
  	extends: ['@commitlint/config-conventional'],
  	rules: {
  		'type-enum': [
  			2,
  			'always',
  			[
  				'build',   // 编译相关的修改，例如发布版本，对项目构建或者依赖的改动
  				'feat',    // 新功能(feature)
  				'fix',     // 修复bug
  				'upd',     // 更新某功能
  				'refactor',// 重构
  				'docs',    // 文档
  				'chore',   // 构建过程或辅助工具的变动，比如增加依赖库等
  				'style',   // 格式（不影响代码运行的变动）
  				'revert',  // 撤销commit,回滚到上一个版本
  				'perf',    // 性能优化
  				'test',    // 测试（单元、集成测试）
  			]
  		],
  		'type-case': [0],
  		'type-empty': [0],
  		'scope-empty': [0],
  		'scope-case': [0],
  		'subject-full-stop': [0, 'never'],
  		'subject-case': [0, 'never'],
  		'header-max-length': [0, 'always', 72],
  	},
  };
  ```

### Step 5 配置vite.config.ts文件

- ```
  pnpm install vite-plugin-eslint vite-plugin-stylelint@^3.1.1 -D
  ```

- 修改文件：

  ```js
  import path from 'path'
  import { defineConfig } from 'vite'
  import vue from '@vitejs/plugin-vue'
  import eslintPlugin from 'vite-plugin-eslint'
  import stylelintPlugin from 'vite-plugin-stylelint'
  
  // https://vitejs.dev/config/
  export default defineConfig({
    plugins: [vue(), eslintPlugin(), stylelintPlugin({ fix: true })],
    resolve: {
      alias: {
        '@': path.resolve(__dirname, './src'),
      },
    },
    server: {
      host: 'localhost',
      // port: 8080,
      open: true,
    },
  })
  
  ```

### Step 6 (可选) 修改tsconfig.json文件

- 为了让tsc支持`@`代表`"./src/"`自动提示补全，设置`baseUrl`和`paths`选项

  ```json
  {
    "compilerOptions": {
      "target": "ESNext",
      "useDefineForClassFields": true,
      "module": "ESNext",
      "moduleResolution": "Node",
      "strict": true,
      "jsx": "preserve",
      "resolveJsonModule": true,
      "isolatedModules": true,
      "esModuleInterop": true,
      "lib": ["ESNext", "DOM"],
      "skipLibCheck": true,
      "noEmit": true,
      "baseUrl": ".",
      "paths": {
        "@/*": ["src/*"]
      }
    },
    "include": ["src/**/*.ts", "src/**/*.d.ts", "src/**/*.tsx", "src/**/*.vue"],
    "references": [{ "path": "./tsconfig.node.json" }]
  }
  
  ```

### 附录 package.json文件

```json
{
  "name": "vite-vuets-app",
  "private": true,
  "version": "0.0.0",
  "type": "module",
  "scripts": {
    "dev": "vite",
    "build": "vue-tsc && vite build",
    "preview": "vite preview",
    "lint": "eslint \"src/**/*.{js,vue,ts}\" --fix",
    "prettier-format": "prettier \"src/**/*.{vue,js,ts}\" --write",
    "lint:css": "stylelint **/*.{vue,css,sass,scss,less} --fix",
    "lint:all": "pnpm run lint && pnpm run prettier-format && pnpm run lint:css",
    "prepare": "husky install"
  },
  "lint-staged": {
    "src/**/*.{js,jsx,vue,ts,tsx}": [
      "eslint --fix",
      "prettier --write"
    ],
    "*.{vue,less,css,sass,scss}": [
      "stylelint --fix"
    ]
  },
  "dependencies": {
    "vue": "^3.2.41"
  },
  "devDependencies": {
    "@commitlint/cli": "^17.3.0",
    "@commitlint/config-conventional": "^17.3.0",
    "@types/node": "^18.11.9",
    "@typescript-eslint/eslint-plugin": "^5.44.0",
    "@typescript-eslint/parser": "^5.44.0",
    "@vitejs/plugin-vue": "^3.2.0",
    "eslint": "^8.28.0",
    "eslint-config-prettier": "^8.5.0",
    "eslint-config-standard": "^17.0.0",
    "eslint-plugin-import": "2.25.2",
    "eslint-plugin-n": "15.0.0",
    "eslint-plugin-promise": "6.0.0",
    "eslint-plugin-vue": "^9.8.0",
    "husky": "^8.0.2",
    "less": "^4.1.3",
    "lint-staged": "^13.0.4",
    "postcss": "^8.4.19",
    "postcss-html": "^1.5.0",
    "prettier": "^2.8.0",
    "stylelint": "^14.15.0",
    "stylelint-config-recommended-less": "^1.0.4",
    "stylelint-config-recommended-scss": "^8.0.0",
    "stylelint-config-recommended-vue": "^1.4.0",
    "stylelint-config-standard": "^29.0.0",
    "typescript": "^4.9.3",
    "vite": "^3.2.3",
    "vite-plugin-eslint": "^1.8.1",
    "vite-plugin-stylelint": "~3.0.10",
    "vue-tsc": "^1.0.9"
  }
}

```

