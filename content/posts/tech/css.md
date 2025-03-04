---
title: '常用 CSS 样式'
date: 2025-03-04
tags: ['技术', 'css']
---

```
.centered {
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%); /* 完全居中对齐 */
}

.vertical-centered {
    position: absolute;
    top: 50%;
    transform: translateY(-50%); /* 仅垂直居中 */
}

.text-ellipsis {
    width: 100px;
    white-space: nowrap;
    overflow: hidden;
    text-overflow: ellipsis; /* 超出部分省略号显示 */
}
```
