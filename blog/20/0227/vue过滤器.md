---
title: 过滤器
date: 2020-02-28 23:40:35
tags: 过滤器
---
### 过滤器

> 过滤器可以理解为给当前数据增添内容

---
```
🌰🌰🌰
html:
<div>{{ price | addContent }}</div>

script:
data: {
    price: 10
}
filters: {
    addContent(price) {
        return price + '¥'
    }
}

输出  10¥
```

这是一个简单的过滤器实现

---
要注意的点有：

1、过滤器可以一直向后极连

2、过滤器只是改变了展示的数据，数据源未改变

3、过滤器中的参数有以下形式

> {{ data | filter1 | filter2 }}

data作为参数先传给filters1函数，filters1函数的返回值在作为参数传给filters2，最终的返回值是filters2的返回值
```
<div>{{ '10' | filter1 | filter2 }}</div>

filters: {
    filter1(val) {
        return val + '元'
    },
    filter2(val) {
        return '总价：' + val
    }
}

输出  总价：10元
```

> {{ data | filter1('arg1', arg2) }}

data作为filter1的第一个参数，之后的参数为arg1,arg2

```
<div>{{ '4' | filter('3', '96') }}</div>

filters: {
    filter1(val,arg1,arg2) {
        return val + arg1 + arg2
    }
}

输出  4396
```
> {{ 'a', 'b' | filter1 }}

a和b分别作为参数传给filter1函数

```
<div>{{ 'clearlove', '7' | filter1 }}</div>

filters: {
    filter1(val1, val2) {
        return val1 + val2
    }
}

输出  clearlove7
```