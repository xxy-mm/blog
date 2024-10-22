---
layout: post
title: "Switch case where in Swift"
---

1. **基本语法结构**
   - 在Swift的`switch`语句中，`case where`的基本语法是在`case`后面跟上要匹配的模式，然后使用`where`关键字来添加额外的条件。其形式如下：

   ```swift
   switch someValue {
       case pattern where condition:
           // 执行的代码块
       case otherPattern:
           // 执行的代码块
       // 其他case分支
   }
   ```

   - 其中`someValue`是要进行判断的值，`pattern`是匹配的模式，`condition`是额外的条件表达式。

2. **示例：判断数字的范围和奇偶性**
   - 假设你有一个整数变量，你想根据它的值所在的范围以及奇偶性进行不同的操作。

   ```swift
   let number = 7
   switch number {
       case let n where n < 0:
           print("\(n)是负数")
       case let n where n >= 0 && n <= 10 && n % 2 == 0:
           print("\(n)是0到10之间的偶数")
       case let n where n >= 0 && n <= 10 && n % 2!= 0:
           print("\(n)是0到10之间的奇数")
       case let n where n > 10 && n % 2 == 0:
           print("\(n)是大于10的偶数")
       case let n where n > 10 && n % 2!= 0:
           print("\(n)是大于10的奇数")
   }
   ```

   - 在这个例子中，首先通过`let n`捕获要判断的数字`number`，然后在`where`条件中判断数字的范围和奇偶性。例如，在第二个`case`中，条件`n >= 0 && n <= 10 && n % 2 == 0`表示数字在0到10之间并且是偶数。

3. **示例：处理枚举类型的复杂情况**
   - 考虑一个表示形状的枚举，它有不同的形状类型，并且每个形状类型可能有不同的属性。

   ```swift
   enum Shape {
       case circle(radius: Double)
       case rectangle(length: Double, width: Double)
       case triangle(base: Double, height: Double)
   }

   let shape: Shape =.circle(radius: 5.0)
   switch shape {
       case.circle(let radius) where radius > 3.0:
           print("这是一个半径大于3.0的圆形")
       case.circle:
           print("这是一个半径小于等于3.0的圆形")
       case.rectangle(let length, let width) where length == width:
           print("这是一个正方形")
       case.rectangle:
           print("这是一个普通矩形")
       case.triangle(let base, let height) where base * height > 10.0:
           print("这是一个面积（0.5*底*高）大于5.0的三角形")
       case.triangle:
           print("这是一个面积（0.5*底*高）小于等于5.0的三角形")
   }
   ```

   - 这里对于枚举`Shape`的`switch`判断，通过`case where`不仅可以匹配形状的类型（如`circle`、`rectangle`、`triangle`），还可以根据形状的具体属性（如圆形的半径、矩形的长和宽、三角形的底和高）来进行更细致的条件判断。