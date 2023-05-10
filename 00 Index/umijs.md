
## 一、权限

## 版本更新问题

```js
// v3版本有导出国际化方法
import { getIntl, useIntl } from 'umi'; 
// v4版本解决如下
pnpm add -D @umijs/plugins //`ntd`, `dva`, `locale` 在 max 项目里自带了，如果用 umi ，需要单独装：
export default {
  plugins: ['@umijs/plugins/dist/antd','@umijs/plugins/dist/locale'], // .umirc.ts
  antd: {}
}
// pnpm run postinstall 重新生成依赖
pnpm run postinstall 
```
