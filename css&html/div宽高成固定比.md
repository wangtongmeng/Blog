 # div 宽高成固定比

利用 css 限制 div 宽高比为 2: 1，内部使用 float: left 或 position: absolute; 脱离文档流，达到视觉上的统一。

```css
.some-div {
  border: 1px solid red;
  width: 100%;
  min-width: 500px;
  height: 0;
  padding-bottom: 50%;
}
```

