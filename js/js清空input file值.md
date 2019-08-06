# js清空input file值

问题：项目进行导入操作，如果第一次导入某个文件会触发导入操作，但是第二次导入重复该文件，不会触发操作。

原因：是因为上一次file里选择的文件路径值与本次选择的文件路径值是一样的，值没有改变所以导致file不会触发submit事件。
解决方案：每次创建完导入数据后把file的路径值清空，但浏览器的安全机制限制不可以直接用js修改file的value为有效值，解决方法是设置file的value为空字符，或者把file的html重新初始化来解决清空的问题。

```js
var file = document.getElementById('openFile');
file.value = '';
```

