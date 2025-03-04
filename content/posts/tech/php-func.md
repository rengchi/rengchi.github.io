---
title: 'PHP 方法'
date: 2025-03-04
tags: ['技术', 'php']
---

> json 格式数据获取

```
<?php

// 从输入流中读取 JSON 数据
$inputData = file_get_contents('php://input');

// 解析 JSON 数据为 PHP 数组
$data = json_decode($inputData, true);
```

> dd

```
function dd() {
    // 设置响应头，确保正确显示字符编码
    header('Content-Type: text/html; charset=UTF-8');
    
    // 获取所有传入的参数
    $args = func_get_args();
    
    echo '<div style="background-color: #222; padding: 10px;">';
    
    foreach ($args as $arg) {
        echo '<div style="
                    background-color: #333; 
                    color: #0f0; 
                    padding: 10px; 
                    margin-bottom: 10px;
                    border-radius: 5px;
                    font-size: 14px; 
                    font-family: monospace;
                    white-space: pre-wrap;
                    word-wrap: break-word;
                    overflow: auto;">';
        echo '<pre>';
        print_r($arg); // 使用 print_r 以更可读的格式输出
        echo '</pre>';
        echo '</div>';
    }
    
    echo '</div>';
    
    die; // 终止脚本执行
}
```

> 十六进制字符串

```
// 秒级十六进制
function generateHexTimestamp() {
    return dechex(time());
}

echo generateHexTimestamp(); // 例如: '65da3f2e'

// 毫秒级十六进制
function generateMilliHexTimestamp() {
    return dechex(round(microtime(true) * 1000));
}

echo generateMilliHexTimestamp(); // 例如: '17f9e3e1b9b'

```

> register_shutdown_function

[使用文档](https://www.php.net/manual/zh/function.register-shutdown-function.php)