## 关键词

关键字、映射类型

## 1 映射类型

### 1.1 Record

把K的属性赋值给类型T，并返回新的类型

```js
type Record<K extends keyof any, T> = { [P in K]: T; };
type proxyKType = Record<K,T> // K 可以是联合类型 枚举类型 
```

### 1.2  Partial

将类型定义的所有属性都修改为可选。

```js
type Coord = Partial<Record<'x' | 'y', number>>;

// 等同于
type Coord = {
	x?: number;
	y?: number;
}
```

### 1.3  Pick

从类型定义的属性中，选取指定一组属性，返回一个新的类型定义。

```js
type Coord = Record<'x' | 'y', number>;
type CoordX = Pick<Coord, 'x'>;

// 等用于
type CoordX = {
	x: number;
}
```