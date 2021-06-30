---
layout: article
title: python字符串格式化
mathjax: true
tags: 技术 
---

python字符串format功能，可以格式化多种形式的字符串。

下面是一些python数字格式化的例子，[原帖地址](https://www.runoob.com/python/att-string-format.html)

| 数字       | 格式    | 输出      | 描述                   |
| ---------- | ------- | --------- | ---------------------- |
| 3.1415926  | {:.2f}  | 3.14      | 保留小数点后两位       |
| 3.1415926  | {:+.2f} | +3.14     | 带符号保留小数点后两位 |
| -1         | {:+.2f} | -1.00     | 带符号保留小数点后两位 |
| 2.71828    | {:.0f}  | 3         | 不保留小数             |
| 5          | {:0>2d} | 05        | 数字左边补零，宽度为2  |
| 5          | {:x<4d} | 5xxx      | 数字右边补x，宽度为4   |
| 10         | {:x<4d} | 10xx      | 数字右边补x，宽度为4   |
| 1000000    | {:,}    | 1,000,000 | 逗号分隔的数字形式     |
| 0.25       | {:.2%}  | 25%       | 百分数形式             |
| 1000000000 | {:.2e}  | 1.00e+09  | 指数计数               |
| 13         | {:>10d} | 13        | 右对齐，宽度为10       |
| 13         | {:<10d} | 13        | 左对齐，宽度为10       |
| 13         | {:^10d} | 13        | 中间对齐，宽度为10     |