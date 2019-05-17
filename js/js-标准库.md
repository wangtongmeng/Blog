# js 标准库

## Date

当天零点时间戳

```js
var timeStamp = new Date(new Date().setHours(0, 0, 0, 0)) / 1000;
```

三天前零点

```js
var ThreeDayAgo = timeStamp - 86400 * n;
```

当天具体时间

```js
new Date().setHours(02, 50, 50, 0) //凌晨2点50分50秒0毫秒
```







