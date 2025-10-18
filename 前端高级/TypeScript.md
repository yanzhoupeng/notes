### 什么是 TypeScript

- TypeScript 是 JavaScript 的超集
- 增加了：静态类型检查、接口、泛型等现代开发特性，适合大型项目的开发

> **为什么是 TypeScript？**
>
> 静态类型检查 - 将错误前置
> 提高可读性和可维护性
> 广泛采用

### TypeScript 编译

> 仅了解，直接使用 vue3 即可

```shell
# 初始化项目
pnpm init

# 安装依赖
pnpm i -D typescript ts-node @types/node

# 初始化 TypeScript 配置文件
npx tsc --init
```

调整 tsconfig.json

```json
{
  "compilerOptions": {
    "target": "ES6", // 目标ECMAScript版本
    "module": "esnext", // 使用esnext模块机制
    "strict": true, // 启用严格模式
    "esModuleInterop": true, // 允许与CommonJS模块互操作

    "outDir": "./dist", // 编译后的输出目录
    "rootDir": "./src", // 源代码目录
    "moduleResolution": "node" // 使用Node.js风格的模块解析
  },
  "include": ["src/**/*"], // 包含的文件 需要根据代码的层级手动修改
  "exclude": ["node_modules"] // 排除的文件
}
```

添加脚本到 package.json

```json
{
  "scripts": {
    "build": "tsc", // 编译TypeScript代码
    "start": "node dist/index.js", // 运行编译后的代码
    "dev": "ts-node src/index.ts", // 开发模式：实时运行TypeScript代码
    "clean": "rm -rf dist" // 清理编译输出目录，for windows: "rmdir /s /q dist"
  }
}
```

### 类型声明

> **类型推断**
>
> TypeScript 会根据变量的值自动推断变量的类型 - 简单的类型不需要特殊标明

#### 示例

```ts
let a: number;
let b: string;
let c: boolean;

const fn = (x: number, y: number): number => {
  return x + y;
};
```

#### 类型总览

- JavaScript 自带
  - string
  - number
  - boolean
  - null
  - undefined
  - bigint
  - symbol
  - object
    - 包括 Array Function Data Error 等对象
- TypeScript 新增的类型
  - any
  - never
  - unknown
  - void
  - tuple
  - 元组
  - enum
  - 枚举
- 用于自定义类型的关键字
  - type
  - interface

#### 注意点

**`string` 和 `String` 的区别：**

`string` 是基础数据类型， `String` 是包装对象
在 JavaScript 中，有一些内置对象，如 Number、String，会创建对应的包装对象，日常开发中很少使用，TypeScript 中也是同理，所以 TypeScript 中进行类型声明时，通常会使用小写的 `string`、`number`

> **为什么存在 `String`**
>
> 自动装箱：JavaScript 在必要时会将原始数据类型包装成对象，以便调用属性或者方法
> 如`let a = 'sss'; console.log(s.length)`

### 常用类型

#### any

> anyscript（不是

any 类型的变量可以赋值给**任意**类型的变量

#### unknown

类型安全的 any，适用于类型暂时无法确定的情况

unknown 的变量不可以赋值给任意类型变量。需要通过**断言**进行赋值

```TS
let test: unknown;

test = 'hello';

const res = (<string>test).substring(1, 2); // 类型断言
```

#### never

never：任何数据类型都不是

- 一般不会用来限制变量
- 可以用来限制函数的返回值--当函数永远无法正常结束的情况
- TypeScript 一般是由主动类型推到得出

#### void

只可以接受 undefined（never 不能接收任何数据类型），void 类型的函数返回值也不应当被使用进行任何操作

- 常用来限制函数返回值

```TS
const fn = (num: number): void => {
	console.log(num);
	// JS 的函数会有一个隐式返回值 undefined
};
```

- void 类型 !== undefined
  - **void 类型的函数返回值不应当被使用进行任何操作**
  - 但是 undefined 类型的函数返回值可以被使用
  - 从抽象的角度来说，void 是 undefined 的超集

#### object

用途较少，因为限制范围过大了

- `object` 可以存储非基础数据类型
- `Object` 可以存储能调用到 Object 方法的所有类型。即除了 null 和 undefined 之外的所有类型
  - 自动装箱

**对象类型限制**

```ts
let obj: {
  id: number;
  name: string;
  age?: number; // 可选变量
  [key: string]: any; // 索引签名
};
```

**声明函数类型**

```TS
let fn = (n1: number, n2: number) => number

fn = (x, y) => { return x + y }
```

**声明数组类型**

```TS
let arr: Array<number> = [1, 2, 2] // 泛型
let arr: number[] = [1, 2, 2]
```

#### tuple

元组（tuple）用来存储**固定数量、数据类型已知且不同**的数组

```ts
let tuple: [number, string]; // 这就是一个元组
let tuple: [number, string?];
let tuple: [number, ...string[]]; // 可以有任意多个 string 类型元素
```

#### enum

定义一组**命名的常量集合**，强调代码可读性和类型安全

```ts
// 数字枚举 带有反向映射
enum Direction {
  Up,
  Down,
  Left,
  Right,
}

// 字符串枚举
enum Direction {
  Up = '上',
  Down = '下',
  Left = '左',
  Right = '右',
}

// 常量枚举 在编译时内联，减少无用代码
const enum Direction {
  Up,
  Down,
  Left,
  Right,
}
```

#### type

类型别名，方便复用

```ts
// 联合类型
// 联合类型需要满足条件之一
type Status = string | number;
type Gender = 'male' | 'female' | 0 | 1;

// 交叉类型
// 交叉类型需要满足所有条件
type Area = { width: number; height: number };
type Address = { id: number; room: string };
type House = Area & Address;
```

#### 类

**类和子类的简单使用**

```ts
class Person {
  private name: string;
  private age: number;

  constructor(name: string, age: number) {
    this.name = name;
    this.age = age;
  }

  greet() {
    console.log(
      `Hello, my name is ${this.name} and I am ${this.age} years old.`
    );
  }
}

class Student extends Person {
  private grade: number;

  constructor(name: string, age: number, grade: number) {
    super(name, age);
    this.grade = grade;
  }

  override greet() {
    console.log(
      `Hello, my name is ${this.name}, I am ${this.age} years old and I am in grade ${this.grade}.`
    );
  }
}
```

**属性的简写**

```TS
class Person {
  // 不额外声明 直接在constructor中同时声明
  constructor(public name: string, public age: number) {}
}
```

**修饰符**

- public
  公开成员，在类的内部、子类、外部均可以使用
- protected
  受保护的成员，类的内部、子类可以使用
- private
  私有成员，只能在类内部访问
- readonly
  只读成员

#### 抽象类

> 抽象类是一种无法被实例化的类，主要目的是定义类的结构和方法，类中可以包含普通方法和抽象方法，其派生类中必须要对抽象方法进行实现

**最佳实践**

- 定义通用接口
- 提供基础实现
- 确保关键实现
- 共享代码和逻辑

```TS
// 抽象类
abstract class Package {
  constructor(public weight: number) {}
  abstract calculate(): number;
  getPackageMsg() {
    console.log(
      `快递包裹重量为 ${this.weight} kg，运费为 ${this.calculate()} 元`
    );
  }
}

// 实现类
class StandardPackage extends Package {
  constructor(weight: number, public unit: number) {
    super(weight);
  }
  calculate(): number {
    return this.weight * this.unit; // 标准快递每公斤5元
  }
}

const standardPackage = new StandardPackage(2, 5);
standardPackage.getPackageMsg();
```

#### interface

**最常使用的定义类型的方式**

- 定义对象格式：描述数据模型、API 相应格式、配置对象
- 类的契约
- 自动合并：用于扩展第三方库的类型

```TS
interface ObjInterface {
	name: string;
	age?: number;
	readonly gender: string;
	speak: () => void;
}
```

##### interface 和 type

- 两者在定义对象时可以等价替换
- 不同点
  - interface 更常用于定义类和对象的结构，支持合并、继承
  - type 可以进行类型别名、类型交叉、联合类型的声明

### 泛型

#### 定义方法

```TS
const fn = <T, U>(data: T, data2: U): T | U => {
  return Math.random() > 0.5 ? data : data2;
};

const res = fn<string, number>('hello', 42);
```

#### 定义接口

```TS
// 通用接口 比如request的基本接口
interface PersonInterface<T> {
  name: string;
  age: number;
  extraMsg: T;
}

// 会用在通用接口的泛型接口
interface EmployeeInterface {
  id: number;
  department: string;
}

const p: PersonInterface<EmployeeInterface> = {
  name: 'Alice',
  age: 30,
  extraMsg: {
    id: 101,
    department: 'Engineering',
  },
};
```

### 接口文件

```TS
// .d.ts
declare const fn: (num: number) => number

export {fn}
```
