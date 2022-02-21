# 类型

在变量后添加 `: type` 声明类型，
大部分情况不用明确声明，TS会自动根据上下文判断。

## 基础

基本原始类型

* string
* number
* boolean
* null
* undefined
* bigint
* symbol

引用类型：

* 数组 `Array[number]`
* 对象，声明每个属性的类型

特殊：

* any
* 字面量，枚举类型
* never 不会处理的地方
* void 函数无返回

## 组合

* 使用 `|` 声明多个类型，操作该值时，必须支持所有类型。比如类型支持 `string` 和 `number` 就用不了 `toUpperCase` 方法，因为 `number` 不支持。如果必须使用，需要在上下文说明，比如 `typeof`。
* 别名，使用 `type` 声明一个类型。不可扩展
* interface，声明类型，可扩展

```ts
interface Animal {
  name: string
}

interface Bear extends Animal {
  honey: boolean
}

type Animal = {
  name: String
}

type Bear = Animal & {
  honey: boolean
}
```

## 类型断言

`TS` 根据上下文判断的类型可能过于宽泛，使用 `as type` 或 `<type>` 定义更具体的类型。

由于对象属性的值可以被改变，对象中的值类型声明需要比使用时更具体。

## 缩圈

* if, switch, which
* typeof
* ===, ==, !=
* in, instanceof
* 声明，根据返回值类型，可能得到组合类型
* 类型预测 `is`

## Function

* `(someAry: paramType): returnType`
* 作为构造函数，在括号前加 `new`
* 多次使用相同的未定义类，TS会认为这几个类型相同，并根据实际情况确定类型
* 可选参数使用 `?:` 或提供默认值，使用第一种方法支持传递undefined
* this需要声明类型

### 重载

明确指明适用场景。
当需要多个可选参数时，需要不同参数数量的场景，可以使用多个定义以 `;` 分割。

尽量使用组合，而不是重载。

## Object

`readonly`，不递归处理，只处理变量，不管引用，可以通过一个新的变量，指向相同引用来修改。

## TODO

* [Generic Functions](https://www.typescriptlang.org/docs/handbook/2/functions.html#generic-functions)
* [optional-parameters](https://www.typescriptlang.org/docs/handbook/2/functions.html#optional-parameters-in-callbacks)
* [Assignability of Functions](https://www.typescriptlang.org/docs/handbook/2/functions.html#assignability-of-functions)
