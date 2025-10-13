
### 什么是 TypeScript

- TypeScript 是 JavaScript 的超集
- 增加了：静态类型检查、接口、泛型等现代开发特性，适合大型项目的开发

>**为什么是 TypeScript？**
>
>静态类型检查 - 将错误前置
>提高可读性和可维护性
>广泛采用

### TypeScript 编译

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

>**类型推断**
>
>TypeScript 会根据变量的值自动推断变量的类型 - 简单的类型不需要特殊标明

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

>**为什么存在 `String`**
>
>自动装箱：JavaScript 在必要时会将原始数据类型包装成对象，以便调用属性或者方法
>如`let a = 'sss'; console.log(s.length)`


### 常用类型

#### any

anyscript（不是

any 类型的变量可以赋值给**任意**类型的变量

#### unknown

类型安全的 any，适用于类型暂时无法确定的情况