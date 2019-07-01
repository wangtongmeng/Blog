# css 元素居中方案

- 水平居中

  - 水平居中-行内元素
  - 水平居中-块级元素
  - 水平居中-多个块级元素

- 垂直居中

  - 垂直居中-行内元素
    - 垂直居中-单行不换行居中
    -  垂直居中-多行整体居中
  - 垂直居中-块级元素

- 水平垂直居中

  - 固定宽高的元素
  - 未知宽高的元素
  - 是否用flexbox
  - 是否用grid

  详细案例：<https://css-tricks.com/centering-css-complete-guide/>

## 水平居中

### 水平居中-行内元素

块级元素内水平居中行内元素

```css
.center-children {
  text-align: center;
}
```

### 水平居中-块级元素

对于有固定宽的块级元素，没有设置固定宽的话，占满父元素。

```css
.center-me {
  margin: 0 auto;
}
```

### 水平居中-多个块级元素

将多个块级元素水平居中到一行

- 方案一，将所有块级元素变为行内元素，并居中
- 方案二，利用 flex 居中

方案一，将所有块级元素变为行内元素，并居中

```css
.inline-block-center {
  text-align: center;
}
.inline-block-center div {
  display: inline-block;
  text-align: left;
}
```

方案二，利用flex 居中

```css
.flex-center {
  display: flex;
  justify-content: center;
}
```

## 垂直居中

### 垂直居中-行内元素

#### 垂直居中-行内元素-单行不换行居中

利用上下 padding 居中

```css
.link {
  padding-top: 30px;
  padding-bottom: 30px;
}
```

对于不换行的行内元素，利用 line-height 等于 height 居中

```css
.center-text-trick {
  height: 100px;
  line-height: 100px;
  white-space: nowrap;
}
```

#### 垂直居中-行内元素--多行整体居中

<p class="codepen" data-height="265" data-theme-id="0" data-default-tab="css,result" data-user="littlebirdflying" data-slug-hash="ZdrdWw" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="ZdrdWw">

