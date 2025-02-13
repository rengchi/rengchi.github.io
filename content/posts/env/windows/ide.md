---
title: 'IDE'
date: 2025-01-20
tags: ['环境', 'windows', 'ide']
description: '编辑器配置相关'
---

# vscode

> settings.json

## 扩展

`Chinese (Simplified) (简体中文) [Microsoft]` `Even Better TOML [tamasfe]` `GitHub Actions [GitHub]` `Go [Go Team at Google]` `Go struct tag liuchao` `HTML CSS Support [ecmel]` `JavaScript(ES6) code snippets [charalampos karypidis]` `Material Icon Theme [Philipp Kief]` `PHP Intelephense [Ben Mewburn]` `Prettier - Code formatter [Prettier]` `Vue - Official [Vue]`

```
{
    // 工作台设置
    "workbench.iconTheme": "material-icon-theme", // material-icon-theme 主题
    "window.zoomLevel": 1.2, // 默认放大窗口 1.2倍
    // 编辑器设置
    "editor.mouseWheelZoom": true, // 鼠标滚轮缩放
    "editor.cursorBlinking": "smooth", // 启用平滑光标呼吸效果
    "editor.cursorSmoothCaretAnimation": "explicit", // 启用光标平滑动画
    "editor.formatOnSave": true, // 启用保存时自动格式化代码
    "editor.snippetSuggestions": "inline", // 优化代码片段建议，插入代码时显示
    "editor.minimap.enabled": false, // 禁用缩略图
    "editor.autoClosingBrackets": "languageDefined", // 根据语言定义自动闭合括号
    "editor.formatOnPaste": true, // 粘贴时自动格式化
    // 启用 IntelliSense 自动补全
    "editor.suggestOnTriggerCharacters": true, // 启用触发字符时的自动补全
    "editor.quickSuggestions": {
        "other": true,
        "comments": true,
        "strings": true
    }, // 启用代码和字符串的自动补全
    "editor.parameterHints.enabled": true, // 启用函数参数提示
    // 启用代码跳转功能
    "editor.gotoLocation.multipleDefinitions": "peek", // 修改为单独的设置
    "editor.gotoLocation.multipleImplementations": "peek", // 修改为单独的设置
    "editor.fontFamily": "'Cascadia Code', monospace", // 默认字体
    // 自动保存设置
    "files.autoSave": "afterDelay", // 延迟后自动保存文件
    "files.autoSaveDelay": 1000, // 自动保存间隔
    // 安全性设置
    "security.workspace.trust.untrustedFiles": "open", // 对于未信任的工作区文件选择打开
    // Prettier 代码格式化设置
    "prettier.tabWidth": 4, // Prettier 格式化时使用 4 个空格缩进
    "prettier.singleQuote": true, // Prettier 使用单引号
    "prettier.printWidth": 100, // 每行的最大字符数，超过这个宽度会换行
    "prettier.semi": false, // 禁用分号
    "prettier.useTabs": true, // 使用 Tab 缩进
    "prettier.endOfLine": "auto", // 自动识别换行符类型
    "prettier.jsxSingleQuote": true, // 在 JSX 中使用单引号
    "prettier.bracketSameLine": true, // JSX 中的闭合标签放在同一行
    // Go 扩展的设置（确保你已经安装了 Go 扩展）
    "go.useLanguageServer": true, // 启用 gopls 语言服务器
    "gopls": {
        "usePlaceholders": true, // 在补全函数时插入占位符
        "staticcheck": true, // 启用 staticcheck 分析工具
        "analyses": {
            "unusedparams": true, // 启用未使用参数的检查
            "shadow": true // 启用变量遮蔽的检查
        }
    },
    // Go 格式化和代码整理设置
    "go.formatTool": "goimports", // 使用 goimports 格式化代码，并自动整理导入
    "go.vetOnSave": "package", // 保存时运行 go vet 检查，范围为当前包
    // Linter 设置，使用 GolangCI-Lint 工具
    "go.lintTool": "golangci-lint", // 配置 GolangCI-Lint 作为 Linter
    "go.lintFlags": [
        "--fast" // 启用快速 lint 检查，减少执行时间
    ],
    "go.lintOnSave": "package", // 保存时自动运行 GolangCI-Lint 对当前包进行检查
    // Go 扩展的测试设置
    "go.testOnSave": true, // 保存时自动运行测试
    "go.testFlags": [
        "-v"
    ],
    "[jsonc]": {
        "editor.defaultFormatter": "vscode.json-language-features" // 测试时使用 -v，显示详细信息
    },
    // go struct teg
    "go-struct-tag.cases": [
        "snake",
        "camel"
    ],
    // JavaScript 相关配置
    "[javascript]": {
        "editor.defaultFormatter": "esbenp.prettier-vscode", // 使用 Prettier 格式化 JavaScript
        "editor.formatOnSave": true, // 保存时自动格式化
        "editor.suggestOnTriggerCharacters": true, // 启用触发字符时的自动补全
        "editor.quickSuggestions": {
            "other": true,
            "comments": true,
            "strings": true
        }, // 启用代码和字符串的自动补全
        "editor.snippetSuggestions": "inline", // 显示代码片段建议
        "editor.parameterHints.enabled": true // 启用函数参数提示
    },
    // CSS 相关配置
    "[css]": {
        "editor.defaultFormatter": "esbenp.prettier-vscode", // 使用 Prettier 格式化 CSS
        "editor.formatOnSave": true, // 保存时自动格式化
        "editor.suggestOnTriggerCharacters": true, // 启用触发字符时的自动补全
        "editor.quickSuggestions": {
            "other": true,
            "comments": true,
            "strings": true
        }, // 启用代码和字符串的自动补全
        "editor.snippetSuggestions": "inline", // 显示代码片段建议
        "editor.parameterHints.enabled": true // 启用函数参数提示
    },
    // Emmet 配置：使其适用于 JavaScript 和 TypeScript
    "emmet.includeLanguages": {
        "javascript": "javascriptreact", // 对 React 使用 Emmet 扩展
        "typescript": "typescriptreact" // 对 TypeScript 使用 Emmet 扩展
    },
    // 启用自动补全（JS 和 CSS）
    "javascript.suggest.autoImports": true, // 启用自动导入建议
    "javascript.suggest.enabled": true, // 启用 JS 自动补全
    "typescript.suggest.autoImports": true, // 启用 TypeScript 的自动导入建议
    "typescript.suggest.enabled": true,
    "[typescript]": {
        "editor.defaultFormatter": "esbenp.prettier-vscode"
    }, // 启用 TypeScript 自动补全
}
```
