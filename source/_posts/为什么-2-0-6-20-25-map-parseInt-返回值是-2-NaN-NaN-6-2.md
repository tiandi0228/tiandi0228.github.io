---
title: '为什么[2,0,6,20,25].map(parseInt)返回值是[2, NaN, NaN, 6, 2]?'
date: 2020-01-13 14:50:26
tags: 
- javascript
- map
- parseInt
---
### 解题：
````
parseInt(2,0)  // 2     0 + 2 = 2
parseInt(0,1) // NaN    1 + 0 = 0 小于2都为NaN
parseInt(6,2) // NaN    二进制 6超出0，1所以是NaN
parseInt(20,3) // 6     2 * 3^1 + 0 * 3^0 = 6
parseInt(25,4) // 2     2 * 4^0 = 2 因为5超出了四进制
````