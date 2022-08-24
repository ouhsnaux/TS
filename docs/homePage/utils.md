# 内置工具泛型

* `Partial` 将属性全部可选，类型全部变为与 `undefined` 的联合类型
* `Required` 全部必选，与 `Partial` 相反
* `ReadOnly` 全部只读
* `Record<Keys, Type>` 属性是 `Keys` 类型，值是 `Type` 类型
* `Pick<Type, Keys>` 从 `Type` 中筛选 `Keys` 类型的属性
* `Omit<Type, Keys>` 从 `Type` 中去除 `Keys` 类型的属性
* `Exclude<UnionType, ExcludedMembers>` 求差集
* `Extract<Type, Union>` 求交集
* `NonNullable` 去空
* `Parameters` 取函数的参数类型
* `ConstructorParameters` 取构造函数的参数列表
* `ReturnType` 取参数的返回值类型
* `InstanceType` // TODO 不太懂，[原文](https://www.typescriptlang.org/docs/handbook/utility-types.html#instancetypetype)
* `ThisParameterType` 获取函数 `this` 的类型
* `OmitThisParameter` 去除 `this` 类型限制
* `ThisType` // TODO 不太懂，[原文](https://www.typescriptlang.org/docs/handbook/utility-types.html#thistypetype)
