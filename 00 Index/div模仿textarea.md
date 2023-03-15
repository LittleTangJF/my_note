## 关键词

contenteditable、resize、overflow、placeholder

## 实现方式

1. 1.  给 div 添加一个HTML全局属性：`contenteditable="true"`，使 div 元素变成用户可编辑的;
2. 1.  给 div 添加样式 `resize: vertical;`，使 div 可以被用户调整尺寸
3. 注意：别忘了设置 `overflow: auto;` 样式，因为resize样式不适用于`overflow: visible`;的块，
4. 1.  增加一个属性：placeholder="I am placeholder"；
5. 1.  通过 CSS 选择器获取并显示 placeholder 的值；