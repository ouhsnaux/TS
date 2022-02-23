# 类型

在变量后添加 `: type` 声明类型，
大部分情况不用明确声明，TS会自动根据上下文判断。

## 基础

### 基本原始类型

* string
* number
* boolean
* null
* undefined
* bigint
* symbol

### 数组

表示方法

* 类型加 `[]`，比如 `number[]`
* 数组泛型 `Array<number>`

#### 元组

数组中可以出现不同类型的数据 `let tom: [string, number];`

* 初始化需要提供所有元素类型中指定的项
* 越界的元素会被限制为元组中所有类型的联合类型

### 函数

* 定义入参和出参的类型，
* 函数表达式需要定义函数，例如
  
    ```ts
    let mySum: (x: number, y: number) => number = function (x: number, y: number): number {
      return x + y;
    };
    ```

* 可选参数，必须在最后
* 参数默认值
* 剩余参数，需要声明为数组
* 重载，当存在多种输入输出且不是所有组合都成立时，枚举输入输出类型组合的情况。

### 特殊

* `any`
* 字面量
* `never` 不会处理的地方
* `void` 函数无返回

## 组合

使用 `|` 声明多个类型，操作该值时，必须支持所有类型。

比如类型支持 `string` 和 `number` 就用不了 `toUpperCase` 方法，因为 `number` 不支持。
如果必须使用，需要在上下文说明，比如 `typeof`。

缺陷：

1. 无法使用变量，如果某个值需要调整，需要遍历整个项目去修改

## 接口 interface

定义对象类型。

```ts
interface Animal {
  name: string
}

interface Bear extends Animal {
  honey: boolean
}
```

* 可选属性，声明时使用 `?:`
* 任意属性
  * `[propName: string]: any;`
  * 确定属性和可选属性必须是该值类型的子集
  * 一个接口只能定义一个。
* readonly

## 类型别名

使用 `type` 声明一个类型，大部分情况下与接口可通用，不可扩展

```ts
type Animal = {
  name: String
}

type Bear = Animal & {
  honey: boolean
}
```

## 枚举 // TODO

`enum`

缺陷：

1. 写法繁杂
2. 编译结果大
3. 无法扩展

## 类 // TODO

## 类型断言

`TS` 可以根据上下文自动判断类型，但是可能过于宽泛，使用类型断言将其精确指定为该类型的子集。

语法：`value as type` 或 `<type> value`。

父类与子类间可以相互断言，所有类型都能与any相互断言。这引出了双重断言，`as any as type`

`as const` 断言对象内部属性不会发生变化。

`!` 断言非空

## 声明文件 .d.ts

<!-- TODO -->
[声明文件](http://ts.xcatliu.com/basics/declaration-files.html#%E6%96%B0%E8%AF%AD%E6%B3%95%E7%B4%A2%E5%BC%95)

声明类型

* `declare var, let, const` 声明全局变量
* `declare function` 声明全局方法
* `declare class` 声明全局类
* `declare enum` 声明全局枚举类型
* `declare namespace` 声明（含有子属性的）全局对象，淘汰
* `interface` 和 `type` 声明全局类型

## TODO 整理

## 类型缩窄

* typeof
* ===, ==, !=
* in, instanceof
* 赋值
* 声明，根据返回值类型，可能得到组合类型
* 类型预测 `is`

## Function

* `(someAry: paramType): returnType`
* 结构签名，构造函数声明在参数括号前加 `new`
* 多次使用相同的未定义类，TS会认为这几个类型相同，并根据实际情况确定类型
* 约束，通过extend可以给泛型添加属性，参数必须包含
* `this` 需要声明类型

## Object

`readonly`，不递归处理，只处理变量，不管引用，可以通过一个新的变量，指向相同引用来修改。

## TODO

* [Generic Functions](https://www.typescriptlang.org/docs/handbook/2/functions.html#generic-functions)
* [optional-parameters](https://www.typescriptlang.org/docs/handbook/2/functions.html#optional-parameters-in-callbacks)
* [Assignability of Functions](https://www.typescriptlang.org/docs/handbook/2/functions.html#assignability-of-functions)

## TODO 进度

<https://www.typescriptlang.org/docs/handbook/2/functions.html#working-with-constrained-values>
