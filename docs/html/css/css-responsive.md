# 响应式网页设计

## 媒体查询

```css
  @media (max-height: 800px) { /* 高度范围在[0, 800px]之间 */
    p {
      font-size: 10px;
    }
  }
```

## 使得图片不要超过页面宽度

```css
    img {
        display: block;
        max-width: 100%;
        height: auto;
    }
```

## 使用viewport相关的大小

```css
<style>
  h2 {
      width: 80vw;
  }
  p {
      width: 75vmin;
  }
</style>
```
