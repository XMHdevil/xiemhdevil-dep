---
title: TypeScript
categories: TS
tags: TS
---

## TypeScript

### 一? 基础类型
1. 布尔值  `let isDone: boolean = false;`
2. 数字  ` let decLiteral: number = 6;`
3. 字符串 `let sentence: string = Hello, my name is ${ name }.`
4. 数组 :  `let list: Array<number> = [1, 2, 3];`
5. 元组 Tuple  : 元组类型允许表示一个已知元素数量和类型的数组，各元素的类型不必相同 ` let x: [string,number];`
6. 枚举 enum :  ??  `enum Color {Red = 1, Green, Blue},let c: Color = Color.Green;`

enum类型是对JavaScript标准数据类型的一个补充。 像C#等其它语言一样，使用枚举类型可以为一组数值赋予友好的名字。
enum Color {Red, Green, Blue}
let c: Color = Color.Green;
默认情况下，从0开始为元素编号。 你也可以手动的指定成员的数值。 例如，我们将上面的例子改成从 1开始编号
enum Color {Red = 1, Green, Blue}
let c: Color = Color.Green;

或者，全部都采用手动赋值：

enum Color {Red = 1, Green = 2, Blue = 4}
let c: Color = Color.Green;

7. any  : 为还不清楚类型的变量指定一个类型 任意类型 ---- > 任何类型

我们会想要为那些在编程阶段还不清楚类型的变量指定一个类型。 这些值可能来自于动态的内容，那么我们可以使用 any类型来标记这些变量：
let notSure: any = 4;
notSure = "maybe a string instead";
notSure = false; // okay, definitely a boolean

8. void : void类型与any类型相反 表示没有任何类型 因为你只能为它赋予undefined和null：

某种程度上来说，void类型像是与any类型相反，它表示没有任何类型。 当一个函数没有返回值时，你通常会见到其返回值类型是 void：
声明一个void类型的变量没有什么大用，因为你只能为它赋予undefined和null：
let unusable: void = undefined;

9. Null 和Undefined 
10. Never : never类型表示的是那些永不存在的值的类型 

never类型表示的是那些永不存在的值的类型。 例如， never类型是那些总是会抛出异常或根本就不会有返回值的函数表达式或箭头函数表达式的返回值类型； 变量也可能是 never类型，当它们被永不为真的类型保护所约束时

11. Object  :    除number，string，boolean，symbol，null或undefined之外的类型。 其一是“尖括号”语法：还有as语法

object表示非原始类型，也就是除number，string，boolean，symbol，null或undefined之外的类型。
使用object类型，就可以更好的表示像Object.create这样的API。
类型断言有两种形式。
let someValue: any = "this is a string";
 其一是“尖括号”语法：
let strLength: number = (<string>someValue).length;
另一个为as语法：
let strLength: number = (someValue as string).length;

12. 类型的断言 :: 有两种方式:
   - 尖括号 let someValue: any = "aaa" let strLength: number = (<string>someValue).length;
   - as 语法 --> let someValue: any = "this is a string";let strLength: number = (someValue as string).length;

> 枚举 ??
> 
```tsx
function warnUser(): void {
    console.log("This is my warning message");
}

```




### 二? 接口
#### 1、可选属性: 选属性名字定义的后面加一个?符号。

接口里的属性不全都是必需的。 有些是只在某些条件下存在，或者根本不存在。 可选属性在应用“option bags”模式时很常用，即给函数传入的参数对象中只有部分属性赋值了。
带有可选属性的接口与普通的接口定义差不多，只是在可选属性名字定义的后面加一个?符号。
可选属性的好处之一是可以对可能存在的属性进行预定义，好处之二是可以捕获引用了不存在的属性时的错误。 比如，我们故意将 createSquare里的color属性名拼错，就会得到一个错误提示：
```ts
interface SquareConfig {
  color?: string;
  width?: number;
}
function createSquare(config: SquareConfig): {color: string; area: number} {
  let newSquare = {color: "white", area: 100};
  if (config.color) {
    newSquare.color = config.color;
  }
  return newSquare;
}
let mySquare = createSquare({color: "black"});
```

#### 2、只读属性
1. readonly 属性名前用 readonly来指定只读属性
一些对象属性只能在对象刚刚创建的时候修改其值。 你可以在属性名前用 readonly来指定只读属性:
```ts
interface Point {
    readonly x: number;
    readonly y: number;
}
```
2. point 赋值一个对象字面量来构造一个Point
你可以通过赋值一个对象字面量来构造一个Point。 赋值后， x和y再也不能被改变了
```ts
let p1: Point = { x: 10, y: 20 };
p1.x = 5; // error!
```
3. ReadonlyArray<T> ReadonlyArray<T>类型，它与Array<T>相似，只是把所有可变方法去掉了
TypeScript具有ReadonlyArray<T>类型，它与Array<T>相似，只是把所有可变方法去掉了，因此可以确保数组创建后再也不能被修改：
```ts
let a: number[] = [1, 2, 3, 4];
let ro: ReadonlyArray<number> = a;
ro[0] = 12; // error!
ro.push(5); // error!
ro.length = 100; // error!
a = ro; // error!
```
#### 3、类 公共私有受保护的修饰符
1. public 成员都默认为 public
  在TypeScript里，成员都默认为 public。
你也可以明确的将一个成员标记成 public。 我们可以用下面的方式来重写上面的 Animal类：
```ts
class Animal {
    public name: string;
    public constructor(theName: string) { this.name = theName; }
    public move(distanceInMeters: number) {
        console.log(`${this.name} moved ${distanceInMeters}m.`);
    }
}
```
2. private 不能在声明它的类的外部访问。
当成员被标记成 private时，它就不能在声明它的类的外部访问。
当我们比较带有 private或 protected成员的类型的时候，情况就不同了。 如果其中一个类型里包含一个 private成员，那么只有当另外一个类型中也存在这样一个 private成员， 并且它们都是来自同一处声明时，我们才认为这两个类型是兼容的。 对于 protected成员也使用这个规则

3. protect protected成员在派生类中仍然可以访问。

4. readonly修饰符 readonly关键字将属性设置为只读的。

readonly关键字将属性设置为只读的。 只读属性必须在声明时或构造函数里被初始化。



### 三? 函数

#### 1、 函数表达式
TS的类型定义中，=> 用来表示函数的定义，左边是输入类型，需要用括号括起来，右边是输出类型。 
```ts
let mySum: (x: number, y: number) => number = function (x: number, y: number): number {
    return x + y;
};
```
#### 2、可选参数
可选参数后面不允许再出现必需参数了
与接口中的可选属性类似，我们用 ? 表示可选的参数
可选参数必须接在必需参数后面。换句话说，可选参数后面不允许再出现必需参数了：
#### 3、剩余参数
可以使用 ...rest 的方式获取函数中的剩余参数（rest 参数）
```ts
function push(array, ...items) {
    items.forEach(function(item) {
        array.push(item);
    });
}

let a = [];
push(a, 1, 2, 3);
```
#### 4、参数默认值
此时就不受「可选参数必须接在必需参数后面」的限制了
我们允许给函数的参数添加默认值，TypeScript 会将添加了默认值的参数识别为可选参数
```ts
function buildName(firstName: string, lastName: string = 'Cat') {
    return firstName + ' ' + lastName;
}
let tomcat = buildName('Tom', 'Cat');
let tom = buildName('Tom');
```
#### 5、函数声明
输入多余的（或者少于要求的）参数，是不被允许的：
一个函数有输入和输出，要在 TypeScript 中对其进行约束，需要把输入和输出都考虑到，其中函数声明的类型定义较简单

### 四? 泛型Generics

我们在函数名后添加了 <T>，其中 T 用来指代任意输入的类型，在后面的输入 value: T 和输出 Array<T> 中即可使用了

#### 1、多个类型参数
```ts
function swap<T, U>(tuple: [T, U]): [U, T] {
    return [tuple[1], tuple[0]];
}

swap([7, 'seven']); // ['seven', 7]

```

#### 2、 泛型约束
采用extends继承接口来实现泛型约束
```ts
interface Lengthwise {
    length: number;
}

function loggingIdentity<T extends Lengthwise>(arg: T): T {
    console.log(arg.length);
    return arg;
}

loggingIdentity(7);
```
#### 3、泛型接口
#### 4、泛型类
```ts
class GenericNumber<T> {
    zeroValue: T;
    add: (x: T, y: T) => T;
}

let myGenericNumber = new GenericNumber<number>();
myGenericNumber.zeroValue = 0;
myGenericNumber.add = function(x, y) { return x + y; };
```

### 五? 类与接口
1. 类实现接口 implements
类实现接口要使用implements
```ts
interface Alarm {
    alert();
}
class Car implements Alarm {
    alert() {
        console.log('Car alert');
    }
}
```
2. 接口继承接口
```ts
interface Alarm {
    alert();
}

interface LightableAlarm extends Alarm {
    lightOn();
    lightOff();
}
```
3. 接口继承类
```ts
class Point {
    x: number;
    y: number;
}

interface Point3d extends Point {
    z: number;
}

let point3d: Point3d = {x: 1, y: 2, z: 3};
```

### 六? 类class
#### 1、访问器修饰符
- public
修饰的属性或方法是公有的，可以在任何地方被访问到，默认所有的属性和方法都是 public 的
- private
修饰的属性或方法是私有的，不能在声明它的类的外部访问
- protect
修饰的属性或方法是受保护的，它和 private 类似，区别是它在子类中也是允许被访问的
- readonly 
只读属性关键字，只允许出现在属性声明或索引签名中。注意如果 readonly 和其他访问修饰符同时存在的话，需要写在其后面
#### 2、抽象类

- 抽象类是不允许被实例化的
- 抽象类中的抽象方法必须被子类实现

```ts
abstract class Animal {
    public name;
    public constructor(name) {
        this.name = name;
    }
    public abstract sayHi();
}

class Cat extends Animal {
    public sayHi() {
        console.log(`Meow, My name is ${this.name}`);
    }
}

let cat = new Cat('Tom');

```

### 七、枚举Enum
#### 1、赋值
- 自动赋值  从0开始递增的数字，对枚举名进行反向映射
```ts
enum Days {Sun, Mon, Tue, Wed, Thu, Fri, Sat};

console.log(Days["Sun"] === 0); // true
console.log(Days["Mon"] === 1); // true
```
- 手动赋值 
enum Days {Sun = 7, Mon = 1, Tue, Wed, Thu, Fri, Sat};
未手动赋值的枚举项会接着上一个枚举项递增。
未手动赋值的枚举项会接着上一个枚举项递增。
手动赋值的枚举项也可以为小数或负数，此时后续未手动赋值的项的递增步长仍为 1
#### 2、常数项和计算所得项
- 常数项 
常数的判断见附录笔记

满足以下条件时，枚举成员被当作是常数：
不具有初始化函数并且之前的枚举成员是常数。在这种情况下，当前枚举成员的值为上一个枚举成员的值加 1。但第一个枚举元素是个例外。如果它没有初始化方法，那么它的初始值为 0。
枚举成员使用常数枚举表达式初始化。常数枚举表达式是 TypeScript 表达式的子集，它可以在编译阶段求值。当一个表达式满足下面条件之一时，它就是一个常数枚举表达式：
数字字面量
引用之前定义的常数枚举成员（可以是在不同的枚举类型中定义的）如果这个成员是在同一个枚举类型中定义的，可以使用非限定名来引用
带括号的常数枚举表达式
+, -, ~ 一元运算符应用于常数枚举表达式
+, -, *, /, %, <<, >>, >>>, &, |, ^ 二元运算符，常数枚举表达式做为其一个操作对象。若常数枚举表达式求值后为 NaN 或 Infinity，则会在编译阶段报错
所有其它情况的枚举成员被当作是需要计算得出的值。

- 计算所得项
通过计算属性做得到的索引，不能在后面接未手动赋值的项
#### 3、常数枚举
const enum  
  常数枚举与普通枚举的区别是，它会在编译阶段被删除，并且不能包含计算成员
```ts
const enum Directions {
    Up,
    Down,
    Left,
    Right
}

let directions = [Directions.Up, Directions.Down, Directions.Left, Directions.Right];
```
#### 4、外部枚举
declare enum 
declare 定义的类型只会用于编译时的检查，编译结果中会被删除
外部枚举与声明语句一样，常出现在声明文件中。

```ts
declare enum Directions {
    Up,
    Down,
    Left,
    Right
}

let directions = [Directions.Up, Directions.Down, Directions.Left, Directions.Right];
```




