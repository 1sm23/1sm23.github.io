---
title: 我的常用css样式
date: 2020-11-02 11:14:07
tags:
- css
- flex layout
---

因为在工程里频繁用到flex布局，所以写了一套常用的flex样式组合
```css
.row{
    display:-webkit-box;
    display:-ms-flexbox;
    display:flex;
    -webkit-box-orient: horizontal;
    -webkit-box-direction: normal;
    -ms-flex-direction: row;
    flex-direction: row;
}
.column{
    display: -webkit-box;
    display: -ms-flexbox;
    display: flex;
}
/* 主轴 */
.justify-between{
    -webkit-box-pack: justify;
    -ms-flex-pack: justify;
    justify-content: space-between;
}
.justify-center{
    -webkit-box-pack: justify;
    -ms-flex-pack: justify;
    justify-content: space-between;
}
.justify-around{
    -ms-flex-pack: distribute;
    justify-content: space-around;
}
/* 交叉轴 */
.item-center{
    -webkit-box-align: center;
    -ms-flex-align: center;
    align-items: center;
}
.item-start{
    -webkit-box-align: start;
    -ms-flex-align: start;
    align-items: flex-start;
}
.item-end{
    -webkit-box-align: end;
    -ms-flex-align: end;
    align-items: flex-end;
}

.grow{
    -webkit-box-flex: 1;
    -ms-flex-positive: 1;
    flex-grow: 1;
}
.shrink{
    -ms-flex-negative: 0;
    flex-shrink: 0;
}

/* 不换行 */
.no-wrap{
    -ms-flex-wrap: nowrap;
    flex-wrap: nowrap;
}
```
这套样式使用`gulp-autoprefixer`处理兼容问题，工程在[flex-layout](https://github.com/1sm23/flex-layout.git)
浏览器兼容为
```json
"browserslist": [
    "> 1%",
    "last 2 versions",
    "not ie <= 8"
  ]
```
其他css重制可以使用[Normalize.css](https://necolas.github.io/normalize.css/)
