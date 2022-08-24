# 模块化

## ESM

### 导出

需要注明 `type` 或 `interface`

```ts
export type Cat = { breed: string; yearOfBirth: number };
 
export interface Dog {
  breeds: string[];
  yearOfBirth: number;
}
```

### 导入

引用文件需要使用同名后缀为 `js` 的文件。

```ts
import { createCatName, type Cat, type Dog } from "./animal.js";
 
export type Animals = Cat | Dog;
const name = createCatName();
```
