### 一行省略

```css
white-space: nowrap;

overflow: hidden;

text-overflow: ellipsis;
```

### 多行行省略

```css
word-break: break-all;

text-overflow: ellipsis;

display: -webkit-box;

-webkit-box-orient: vertical;

-webkit-line-clamp: 2; /* 这里是超出几行省略 */

overflow: hidden;
```