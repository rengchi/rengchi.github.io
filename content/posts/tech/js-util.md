---
title: 'JS 方法'
date: 2025-03-04
tags: ['技术', 'js']
---

> 相差天数

```
function calculateDayDifference(deliveryTime) {
    // 将传入的日期字符串转换为 Date 对象
    let deliveryDate = new Date(deliveryTime);
    let currentDate = new Date();

    // 将时间部分归零，以便仅比较日期部分
    deliveryDate.setHours(0, 0, 0, 0);
    currentDate.setHours(0, 0, 0, 0);

    // 计算两个日期之间的毫秒级时间差
    let timeDifference = deliveryDate.getTime() - currentDate.getTime();

    // 将时间差转换为天数，并返回
    return Math.floor(timeDifference / (1000 * 60 * 60 * 24));
}
```

> 当前日期

```
function formatNumber(num) {
    return String(num).padStart(2, '0');
}

function formatDate(date = new Date(), format = 'YYYY-MM-DD HH:mm:ss') {
    const replacements = {
        YYYY: date.getFullYear(),
        MM: formatNumber(date.getMonth() + 1),
        DD: formatNumber(date.getDate()),
        HH: formatNumber(date.getHours()),
        mm: formatNumber(date.getMinutes()),
        ss: formatNumber(date.getSeconds())
    };

    return format.replace(/YYYY|MM|DD|HH|mm|ss/g, match => replacements[match]);
}

console.log(formatDate());                    // 默认格式: 2024-03-04 14:30:15
console.log(formatDate(new Date(), 'MM/DD')); // 03/04
console.log(formatDate(new Date(), 'HH:mm')); // 14:30
```

> 复选框选中状态

```
function updateCheckboxState(masterCheckboxId, containerClass) {
    // 获取主复选框关联的 name 属性值
    var checkboxName = $(masterCheckboxId).data('name');

    // 获取容器内所有匹配的复选框
    var checkboxes = $(containerClass).find("input[name='" + checkboxName + "']");
    var checkedCount = checkboxes.filter(":checked").length;
    var totalCount = checkboxes.length;

    // 根据选中数量更新主复选框状态
    if (checkedCount === 0) {
        $(masterCheckboxId).prop({ checked: false, indeterminate: false });
    } else if (checkedCount === totalCount) {
        $(masterCheckboxId).prop({ checked: true, indeterminate: false });
    } else {
        $(masterCheckboxId).prop({ checked: false, indeterminate: true });
    }
}
```

> 十六进制字符串

```
// 秒级十六进制
function generateHexTimestamp() {
    return Math.floor(Date.now() / 1000).toString(16);
}

console.log(generateHexTimestamp()); // 例如: '65da3f2e'

// 毫秒级十六进制
function generateMilliHexTimestamp() {
    return Date.now().toString(16);
}

console.log(generateMilliHexTimestamp()); // 例如: '17f9e3e1b9b'

```