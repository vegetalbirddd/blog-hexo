---
title: 布局
date: 2023-04-27 22:00:41
tags:
categories: css
---

# 布局

## flex布局

### flex元素的自动宽度

flex-basis:auto

**witdth:max-content**：最大宽度一直不换行

**witdth:min-content**：最小宽度是这段word中单词最长的那个

### flex元素增大逻辑

```css
父元素{
    display: flex;
    width: 500px;
}
子元素 {
    flex-basis: 50px;/*各个子元素的基础大小*/
    flex-grow: 1; /*子元素的增大占比（1x，x的数值大小见下面公式）*/
    /* 5*(50px + 1x) = 500px  x = 50px  5指有5个增大比为1的子元素*/
}
```

### flex元素缩小逻辑

```css
父元素{
    display: flex;
    width: 500px;
}
子元素 {
    flex-basis: 200px;/*各个子元素的基础大小*/
    flex-shrink: 2; /*子元素的缩小占比（2x，x的数值大小见下面公式）*/
    /* 1000px - 5 * 2x = 500px   x = 50px
       200px - 2 * 50px = 100px 最后子元素的大小
       1000为5个子元素*200所得
    */
}
```

### flex容器的交叉轴对齐

**align-items属性**

