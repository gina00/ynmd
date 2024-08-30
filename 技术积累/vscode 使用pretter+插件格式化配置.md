# vscode 使用pretter+插件格式化配置
```js
// --run--
{
  "git.autofetch": true,
  "editor.formatOnSave": true,
  "eslint.enable": true,
  "eslint.run": "onType",
  "eslint.options": {
    "extensions": [".js", ".vue", ".jsx", ".tsx"]
  },
  "editor.codeActionsOnSave": {

    "source.fixAll.eslint": "explicit"
  },
  "workbench.colorTheme": "Monokai",
  "diffEditor.ignoreTrimWhitespace": false,
  "eslint.validate": [
    "javascript",
    "javascriptreact",
    "vue",
    {
      "language": "html",
      "autoFix": true
    },
    {
      "language": "vue",
      "autoFix": true
    }
  ],
    "editor.accessibilitySupport": "on",
  "vue.codeActions.savingTimeLimit": 100000,
  "git.openRepositoryInParentFolders": "always",
  "[html]": {
    "editor.defaultFormatter": "vscode.html-language-features"
  },
  "editor.unicodeHighlight.invisibleCharacters": false,
  "editor.unicodeHighlight.ambiguousCharacters": false,
  "[vue]": {
    "editor.defaultFormatter": "svipas.prettier-plus"
  },
  "eslint.codeActionsOnSave.rules": null,
  // Use 'prettier-eslint' instead of 'prettier
  "prettier.eslintIntegration": true, // 让prettier使用eslint的代码格式进行校验
  "prettier.semi": false, //去掉代码结尾的分号
  "prettier.singleQuote": true, //使用单引号替代双引号
  "prettier.arrowParens": "avoid",
  "javascript.format.insertSpaceBeforeFunctionParenthesis": true, //让函数(名)和后面的括号之间加个空格
  "vetur.format.defaultFormatter.html": "js-beautify-html", //格式化.vue中html
  "vetur.format.defaultFormatter.js": "vscode-typescript", //让vue中的js按编辑器自带的ts格式进行格式化
  "vetur.format.defaultFormatterOptions": {
    "js-beautify-html": {
      // "wrap_attributes": "force-aligned", //属性强制折行对齐
      "wrap_line_length": 140,
      "wrap_attributes": "auto",
      "end_with_newline": false
    }
  },
  "emmet.triggerExpansionOnTab": true,
  "git.enableSmartCommit": true,
  "liveServer.settings.donotShowInfoMsg": true,
  "[javascript]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },
  "editor.stickyScroll.enabled": false,
  "Lingma.LocalStoragePath": "C:\\Users\\chenj\\.lingma",
  "terminal.integrated.defaultProfile.osx": ""
}

```

