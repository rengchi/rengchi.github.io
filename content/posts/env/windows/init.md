---
title: 'Windows 重装相关'
date: 2025-01-19
tags: ['windows']
description: '重装Windows后准备，避免数据全部存储在C盘'
---

## 写在前面

> **_!注_** 命令中的 `rengchi` 为你的 `windows` 电脑上的 `用户名`，不一定是 `rengchi`

> **_c 盘下的目录并非全部都可以移动，请不要随意使用 `mklink /j` 移动 c 盘数据/目录_**

## 命令

```
mkdir "D:\data" 2>null
mkdir "D:\data\captura" 2>null
mkdir "D:\data\git" 2>null
mkdir "D:\data\go" 2>null
mkdir "D:\data\mysql" 2>null
mkdir "D:\data\nvm" 2>null
mkdir "D:\data\php" 2>null
mkdir "D:\data\tencent" 2>null
mkdir "D:\data\vue" 2>null
mkdir "D:\backup" 2>null
mkdir "D:\temp" 2>null
mkdir "D:\tmp" 2>null
mkdir "D:\env" 2>null
mkdir "D:\logs" 2>null
mkdir "D:\other" 2>null
mkdir "D:\proj" 2>null
mkdir "D:\soft" 2>null


mkdir "D:\c\Program Files\Huawei" 2>nul
mkdir "D:\c\Program Files\Google" 2>nul
mkdir "D:\c\Program Files (x86)\Google" 2>nul
mkdir "D:\c\Program Files (x86)\Huawei" 2>nul
mkdir "D:\c\Program Files (x86)\Tencent" 2>nul
mkdir "D:\c\Program Files (x86)\WXWork" 2>nul
mkdir "D:\c\ProgramData\Huawei" 2>nul
mkdir "D:\c\ProgramData\chocolatey" 2>nul
mkdir "D:\c\ProgramData\ChocolateyHttpCache" 2>nul
mkdir "D:\c\ProgramData\Tencent" 2>nul

mklink /j "C:\Program Files\Huawei" "D:\c\Program Files\Huawei" 2>nul
mklink /j "C:\Program Files\Google" "D:\c\Program Files\Google"
mklink /j "C:\Program Files (x86)\Google" "D:\c\Program Files (x86)\Google" 2>nul
mklink /j "C:\Program Files (x86)\Huawei" "D:\c\Program Files (x86)\Huawei" 2>nul
mklink /j "C:\Program Files (x86)\Tencent" "D:\c\Program Files (x86)\Tencent" 2>nul
mklink /j "C:\Program Files (x86)\WXWork" "D:\c\Program Files (x86)\WXWork" 2>nul
mklink /j "C:\ProgramData\Huawei" "D:\c\ProgramData\Huawei" 2>nul
mklink /j "C:\ProgramData\chocolatey" "D:\c\ProgramData\chocolatey" 2>nul
mklink /j "C:\ProgramData\ChocolateyHttpCache" "D:\c\ProgramData\ChocolateyHttpCache" 2>nul
mklink /j "C:\ProgramData\Tencent" "D:\c\ProgramData\Tencent"

mkdir "D:\rengchi\.chocolatey" 2>nul
mkdir "D:\rengchi\.vscode" 2>nul
mkdir "D:\rengchi\.codearts" 2>nul

mklink /j "C:\Users\rengchi\.chocolatey" "D:\rengchi\.chocolatey" 2>nul
mklink /j "C:\Users\rengchi\.vscode" "D:\rengchi\.vscode" 2>nul
mklink /j "C:\Users\rengchi\.codearts" "D:\rengchi\.codearts" 2>null

mkdir "D:\rengchi\AppData\Local\Adobe" 2>nul
mkdir "D:\rengchi\AppData\Local\another-redis-desktop-manager-updater" 2>nul
mkdir "D:\rengchi\AppData\Local\apifox-updater" 2>nul
mkdir "D:\rengchi\AppData\Local\CEF" 2>nul
mkdir "D:\rengchi\AppData\Local\CodeArtsTemp" 2>nul
mkdir "D:\rengchi\AppData\Local\Composer" 2>nul
mkdir "D:\rengchi\AppData\Local\Deloyment" 2>nul
mkdir "D:\rengchi\AppData\Local\golangci-lint" 2>nul
mkdir "D:\rengchi\AppData\Local\Google" 2>nul
mkdir "D:\rengchi\AppData\Local\gopls" 2>nul
mkdir "D:\rengchi\AppData\Local\hugo_cache" 2>nul
mkdir "D:\rengchi\AppData\Local\npm-cache" 2>nul
mkdir "D:\rengchi\AppData\Local\OfficePLUS" 2>nul
mkdir "D:\rengchi\AppData\Local\PDFgear" 2>nul
mkdir "D:\rengchi\AppData\Local\pnpm" 2>nul
mkdir "D:\rengchi\AppData\Local\pnpm-cache" 2>nul
mkdir "D:\rengchi\AppData\Local\pnpm-state" 2>nul
mkdir "D:\rengchi\AppData\Local\Programs" 2>nul
mkdir "D:\rengchi\AppData\Local\Sublime Text" 2>nul
mkdir "D:\rengchi\AppData\Local\Temp" 2>nul
mkdir "D:\rengchi\AppData\Local\Tencent" 2>nul
mkdir "D:\rengchi\AppData\Local\wxworkweb" 2>nul
mkdir "D:\rengchi\AppData\Local\xmind-updater" 2>nul
mkdir "D:\rengchi\AppData\Local\xwalk" 2>nul
mkdir "D:\rengchi\AppData\Local\Yarn" 2>nul
mkdir "D:\rengchi\AppData\Local\zig" 2>nul
mkdir "D:\rengchi\AppData\Local\微信开发者工具" 2>nul
mkdir "D:\rengchi\AppData\Local\ChromeExtensionCache" 2>nul
mkdir "D:\rengchi\AppData\Local\VirtualStore" 2>nul
mkdir "D:\rengchi\AppData\Local\Huawei" 2>nul


mklink /j "C:\Users\rengchi\AppData\Local\Adobe" "D:\rengchi\AppData\Local\Adobe" 2>nul
mklink /j "C:\Users\rengchi\AppData\Local\another-redis-desktop-manager-updater" "D:\rengchi\AppData\Local\another-redis-desktop-manager-updater" 2>nul
mklink /j "C:\Users\rengchi\AppData\Local\apifox-updater" "D:\rengchi\AppData\Local\apifox-updater" 2>nul
mklink /j "C:\Users\rengchi\AppData\Local\CEF" "D:\rengchi\AppData\Local\CEF" 2>nul
mklink /j "C:\Users\rengchi\AppData\Local\CodeArtsTemp" "D:\rengchi\AppData\Local\CodeArtsTemp" 2>nul
mklink /j "C:\Users\rengchi\AppData\Local\Composer" "D:\rengchi\AppData\Local\Composer" 2>nul
mklink /j "C:\Users\rengchi\AppData\Local\Deloyment" "D:\rengchi\AppData\Local\Deloyment" 2>nul
mklink /j "C:\Users\rengchi\AppData\Local\golangci-lint" "D:\rengchi\AppData\Local\golangci-lint" 2>nul
mklink /j "C:\Users\rengchi\AppData\Local\Google" "D:\rengchi\AppData\Local\Google" 2>nul
mklink /j "C:\Users\rengchi\AppData\Local\gopls" "D:\rengchi\AppData\Local\gopls" 2>nul
mklink /j "C:\Users\rengchi\AppData\Local\hugo_cache" "D:\rengchi\AppData\Local\hugo_cache" 2>nul
mklink /j "C:\Users\rengchi\AppData\Local\npm-cache" "D:\rengchi\AppData\Local\npm-cache" 2>nul
mklink /j "C:\Users\rengchi\AppData\Local\OfficePLUS" "D:\rengchi\AppData\Local\OfficePLUS" 2>nul
mklink /j "C:\Users\rengchi\AppData\Local\PDFgear" "D:\rengchi\AppData\Local\PDFgear" 2>nul
mklink /j "C:\Users\rengchi\AppData\Local\pnpm" "D:\rengchi\AppData\Local\pnpm" 2>nul
mklink /j "C:\Users\rengchi\AppData\Local\pnpm-cache" "D:\rengchi\AppData\Local\pnpm-cache" 2>nul
mklink /j "C:\Users\rengchi\AppData\Local\pnpm-state" "D:\rengchi\AppData\Local\pnpm-state" 2>nul
mklink /j "C:\Users\rengchi\AppData\Local\Programs" "D:\rengchi\AppData\Local\Programs" 2>nul
mklink /j "C:\Users\rengchi\AppData\Local\Sublime Text" "D:\rengchi\AppData\Local\Sublime Text" 2>nul
mklink /j "C:\Users\rengchi\AppData\Local\Temp" "D:\rengchi\AppData\Local\Temp" 2>nul
mklink /j "C:\Users\rengchi\AppData\Local\Tencent" "D:\rengchi\AppData\Local\Tencent" 2>nul
mklink /j "C:\Users\rengchi\AppData\Local\wxworkweb" "D:\rengchi\AppData\Local\wxworkweb" 2>nul
mklink /j "C:\Users\rengchi\AppData\Local\xmind-updater" "D:\rengchi\AppData\Local\xmind-updater" 2>nul
mklink /j "C:\Users\rengchi\AppData\Local\xwalk" "D:\rengchi\AppData\Local\xwalk" 2>nul
mklink /j "C:\Users\rengchi\AppData\Local\Yarn" "D:\rengchi\AppData\Local\Yarn" 2>nul
mklink /j "C:\Users\rengchi\AppData\Local\zig" "D:\rengchi\AppData\Local\zig" 2>nul
mklink /j "C:\Users\rengchi\AppData\Local\微信开发者工具" "D:\rengchi\AppData\Local\微信开发者工具" 2>nul
mklink /j "C:\Users\rengchi\AppData\Local\ChromeExtensionCache" "D:\rengchi\AppData\Local\ChromeExtensionCache" 2>nul
mklink /j "C:\Users\rengchi\AppData\Local\VirtualStore" "D:\rengchi\AppData\Local\VirtualStore" 2>nul
mklink /j "C:\Users\rengchi\AppData\Local\Huawei" "D:\rengchi\AppData\Local\Huawei"

mkdir "D:\rengchi\AppData\Roaming\360Safe" 2>nul
mkdir "D:\rengchi\AppData\Roaming\Adobe" 2>nul
mkdir "D:\rengchi\AppData\Roaming\another-redis-desktop-manager" 2>nul
mkdir "D:\rengchi\AppData\Roaming\apifox" 2>nul
mkdir "D:\rengchi\AppData\Roaming\Captura" 2>nul
mkdir "D:\rengchi\AppData\Roaming\Code" 2>nul
mkdir "D:\rengchi\AppData\Roaming\Composer" 2>nul
mkdir "D:\rengchi\AppData\Roaming\go" 2>nul
mkdir "D:\rengchi\AppData\Roaming\Google" 2>nul
mkdir "D:\rengchi\AppData\Roaming\gopls" 2>nul
mkdir "D:\rengchi\AppData\Roaming\SQLyog" 2>nul
mkdir "D:\rengchi\AppData\Roaming\Sublime Text" 2>nul
mkdir "D:\rengchi\AppData\Roaming\Tencent" 2>nul
mkdir "D:\rengchi\AppData\Roaming\VoipNNModel" 2>nul
mkdir "D:\rengchi\AppData\Roaming\WXDrive" 2>nul
mkdir "D:\rengchi\AppData\Roaming\Xmind" 2>nul
mkdir "D:\rengchi\AppData\Roaming\Huawei" 2>nul
mkdir "D:\rengchi\AppData\Roaming\CodeArts" 2>nul


mklink /j "C:\Users\rengchi\AppData\Roaming\360Safe" "D:\rengchi\AppData\Roaming\360Safe" 2>nul
mklink /j "C:\Users\rengchi\AppData\Roaming\Adobe" "D:\rengchi\AppData\Roaming\Adobe"
mklink /j "C:\Users\rengchi\AppData\Roaming\another-redis-desktop-manager" "D:\rengchi\AppData\Roaming\another-redis-desktop-manager" 2>nul
mklink /j "C:\Users\rengchi\AppData\Roaming\apifox" "D:\rengchi\AppData\Roaming\apifox" 2>nul
mklink /j "C:\Users\rengchi\AppData\Roaming\Captura" "D:\rengchi\AppData\Roaming\Captura" 2>nul
mklink /j "C:\Users\rengchi\AppData\Roaming\Code" "D:\rengchi\AppData\Roaming\Code" 2>nul
mklink /j "C:\Users\rengchi\AppData\Roaming\Composer" "D:\rengchi\AppData\Roaming\Composer" 2>nul
mklink /j "C:\Users\rengchi\AppData\Roaming\go" "D:\rengchi\AppData\Roaming\go" 2>nul
mklink /j "C:\Users\rengchi\AppData\Roaming\Google" "D:\rengchi\AppData\Roaming\Google" 2>nul
mklink /j "C:\Users\rengchi\AppData\Roaming\gopls" "D:\rengchi\AppData\Roaming\gopls" 2>nul
mklink /j "C:\Users\rengchi\AppData\Roaming\SQLyog" "D:\rengchi\AppData\Roaming\SQLyog" 2>nul
mklink /j "C:\Users\rengchi\AppData\Roaming\Sublime Text" "D:\rengchi\AppData\Roaming\Sublime Text" 2>nul
mklink /j "C:\Users\rengchi\AppData\Roaming\Tencent" "D:\rengchi\AppData\Roaming\Tencent" 2>nul
mklink /j "C:\Users\rengchi\AppData\Roaming\VoipNNModel" "D:\rengchi\AppData\Roaming\VoipNNModel" 2>nul
mklink /j "C:\Users\rengchi\AppData\Roaming\WXDrive" "D:\rengchi\AppData\Roaming\WXDrive" 2>nul
mklink /j "C:\Users\rengchi\AppData\Roaming\Xmind" "D:\rengchi\AppData\Roaming\Xmind" 2>nul
mklink /j "C:\Users\rengchi\AppData\Roaming\Huawei" "D:\rengchi\AppData\Roaming\Huawei"
mklink /j "C:\Users\rengchi\AppData\Roaming\CodeArts" "D:\rengchi\AppData\Roaming\CodeArts" 2>null
```
