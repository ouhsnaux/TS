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

确定数组包含元素数量及每个元素的类型。

* 内部支持使用解构 `type StringNumberBooleans = [string, number, ...boolean[]];`
* 初始化需要严格按照类型赋值，不允许越界
* 后续操作允许越界，类型为元组中所有类型的联合类型
* 支持readonly，效果与 `数组 as const` 相同

### 函数

* 定义入参和出参
* 函数表达式需要定义，例如
  
    ```ts
    let mySum: (x: number, y: number) => number = function (x: number, y: number): number {
      return x + y;
    };
    ```

#### 参数

* 定义入参和出参的类型，`(arg: paramType): returnType`
* 可选参数
  * `?:` 必须在最后
  * 提供默认值
* 剩余参数，需要声明为数组，调用时使用 `...` 可能需要 `as const`
* 约束，通过 `extend` 可以给泛型添加属性，入参必须包含该属性
* 参数中回调函数的声明约束的是此函数中调用回调，而不是调用此函数时传递的回调
  * 回调的参数声明一般不用可选参数，除非此函数函数体中调用时可不传
* 参数解构，在结构后声明类型，注意不能在括号内使用`:` 与 `js` 语法冲突

    ```ts
    type ABC = { a: number; b: number; c: number };
    function sum({ a, b, c }: ABC) {
      console.log(a + b + c);
    }
    ```

#### 泛型

用来描述两个值之间类型相关。入参之间，或与出参类型相关。

调用函数时可以手动指明泛型类型。

使用原则：

* 使用泛型本身的功能，尽量避免约束
* 使用更少的泛型变量
* 至少使用2次（不算声明），否则很可能不需要

#### 重载

实现一个函数，实现多种出入参组合的情况。

* 一个实现签名。
* 大于等于2个重载签名，函数内不可见
* 实现签名必须兼容所有重载签名

#### 其它

* 结构签名，构造函数声明在参数括号前加 `new`
* 如果需要使用 `this` 可以在参数中声明类型

### 对象

#### 修饰符

* 可选属性 `?:`
* readonly，属性只读，但是可以修改子属性。可以通过别名绕过
* 索引签名，指明索引类型及值类型 `{ [index: number]: string}`，需要兼容相同类型

#### 泛型

用于生成特定对象类型。

一个Box类型，含有contents，类型与传入类型相同

```ts
interface Box<Type> {
  contents: Type;
}

let box: Box<string>
```

内置对象泛型包括 `Array, Map, Set, Promise, ReadOnlyArray`

### 特殊

* `any`
* 字面量
* `never` 不会处理的地方
* `void` 函数无返回
* `unknown`
* object
* Function

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
* 使用 `extend` 集成，可以同时继承多个

    ```ts
    interface BasicAddress {
      name?: string;
      street: string;
      city: string;
      country: string;
      postalCode: string;
    }
    
    interface AddressWithUnit extends BasicAddress {
      unit: string;
    }
    ```

## 类型别名

使用 `type` 声明一个类型，大部分情况下与接口可通用，不可扩展。
可以使用 `&` 组合新类型

```ts
type Animal = {
  name: String
}

type Bear = Animal & {
  honey: boolean
}
```

继承与交叉的区别在于存在相同属性时的处理

1. 扩展属性必须是被继承属性的子集
2. 组合会取两者的交集

## 枚举 // TODO

`enum`

缺陷：

1. 写法繁杂
2. 编译结果大
3. 无法扩展

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

## Object

`readonly`，不递归处理，只处理变量，不管引用，可以通过一个新的变量，指向相同引用来修改。

## TODO

* It is possible to support both types of indexers...
* [Generic Functions](https://www.typescriptlang.org/docs/handbook/2/functions.html#generic-functions)
* [optional-parameters](https://www.typescriptlang.org/docs/handbook/2/functions.html#optional-parameters-in-callbacks)
* [Assignability of Functions](https://www.typescriptlang.org/docs/handbook/2/functions.html#assignability-of-functions)

## TODO 进度

[<https://www.typescriptlang.org/docs/handbook/2/functions.html#working-with-constrained-values>](https://www.typescriptlang.org/docs/handbook/2/indexed-access-types.html)
