## Vue

#### 对 Vue 的理解

Vue 是一种单页应用的开发框架，有三个核心特性

数据驱动、组件化和指令系统

数据驱动实现了数据的双向绑定，组件化通过封装组件实现了开发逻辑的解耦，提高了代码的可维护性，便于调试。指令系统便于操作 DOM 元素

#### MVVM 的理解

MVVM
MVVM 是前端的开发架构，是 Model - View - ViewModel 的缩写
Model 指模型，即 data 中的数据
View 是视图，用户界面
ViewModel 是 Vue 的实例对象，是连接 View 和 Model 的桥梁

MVVM 的核心就在于数据的双向绑定，在数据改变时，ViewModel 监听到数据的变化，自动更新视图。用户操作视图是，ViewModel 监听到用户的操作，改变数据，实现数据的双向绑定

#### SPA 首页优化

SPA 指的是动态重写当前页面来实现页面交互，避免页面切换导致的用户体验下降

一个 SPA 应用由主页面和多个页面片段组成，通过 Ajax 进行局部刷新，URL 模式一般是哈希模式

SPA 首页优化：减小首页文件体积、路由懒加载、图片懒加载、gzip 打包、图片资源压缩 svg、cdn 加载第三方资源、SSR 服务端预渲染

#### v-if 和 v-show

v-if 和 v-show 都可以控制元素的显示隐藏，区别在于，v-if 的本质是对 DOM 元素的挂载和卸载，v-show 则是通过 display 属性控制元素的显示隐藏。因此，v-if 会触发元素和子组件的生命周期事件，v-show 不会，同时 v-if 的性能会比 v-show 低一些

#### v-for 的 key

key 是 DOM 元素的唯一标识，主要用于优化虚拟 DOM 的更新过程，它可以帮助 Vue 识别那些元素是可复用的

没有 key 时，Vue 会采取‘就地更新’策略，有可能导致状态错乱
有 key 时，Vue 能准确识别节点的移动，进行最小化的 DOM 操作

#### v-if 和 v-for

v-for 的优先级比 v-if 的高。同时两者不建议一起使用，可以通过 template 标签包裹住 v-for 的元素，不然会造成性能上的浪费

#### vue 生命周期

组件由创建到销毁的过程

创建、挂载、更新、销毁、keep-alive
beforeCreate、created，beforeMount、mounted，beforeUpdate、Updated，beforeDestroy、destroyed，activited、deActivited

Created 生命周期中常用来进行 data 的访问，异步数据的请求
mounted 用于进行数据访问和 DOM 操作
beforeDestroy 常用来销毁定时器

Vue3 去掉了 beforeCreate 和 created，改为了 setup

> **Created 和 Mounted 中有什么区别**
>
> Created 生命周期中 DOM 未进行渲染，mounted 是在 DOM 渲染完毕后，可以直接操作 DOM 元素
> 所以一般会在 Created 中进行数据请求，在 mounted 中请求的数据如果对 DOM 有影响，就会导致闪屏的现象

#### computed 和 watch

computed 是计算属性，watch 是监听
computed 支持缓存，会在数值未改变的情况下自动读取缓存中的数据，watch 不支持缓存
computed 不支持异步，watch 支持异步操作
watch 可能导致循环监听，导致内存溢出，一般会尽可能减少使用

#### vue 指令修饰符

vue 的指令修饰符包括五类：表单、鼠标、键盘、v-bind 和事件修饰符

常用的有：

事件修饰符
.stop：阻止事件冒泡
.prevent：阻止元素的默认行为
.once
.native：使组件可以监听原生事件

按键
.keyup
.keydown

表单
.lazy：在 input 输入完成后进行同步
.trim：去除空格
.number：自动转换成数值类型

#### vue 实例挂载

#### vue 组件通信

props：组件中定义 props，父组件调用时传入对应的值
emits：子组件通过 emits 向父组件暴露方法，父组件在调用子组件时进行时间监听

refs：子组件向外暴露方法或属性，父组件可以通过访问子组件的 ref 访问对应的属性和方法

pinia：state（ref）是共享的数据、getter（computed）是对数据的处理，actions 是修改数据的方法，包括同步和异步方法

#### vue 插槽

普通插槽 slot，父组件可以通过 template 直接使用
具名插槽，name 属性，父组件可以使用#name 使用
作用域插槽，可以在 slot 上添加自定义属性，向父组件传递数据

#### keep-alive

keep-alive 包裹的组件，在关闭后不会销毁，而是缓存下来保存在内存中，可以防止重复渲染 DOM

具有 includes，只有符合名称的组件会被缓存
max，定义了可以缓存的最大组件数（LRU 算法，最近最少使用）

在每次打开缓存的组件时，可以通过 activite 生命周期更新获取数据

#### 自定义指令

#### 虚拟 DOM 和 diff 算法

虚拟 DOM 就是通过 JS 的对象来描述一个 元素

真实的 DOM 元素上具有很多的属性，所以直接操作真实 DOM 元素就会产生很大的性能浪费
通过虚拟 DOM，更新 DOM 时不会直接操作 DOM 元素，而是将所有更新的 diff 存储到一个对象中，最终将这个对象一次性 attach 到 DOM 树上，避免了大量无用的计算

#### aixos

首先使用 create 对 axios 进行实例化，并配置过期时间和请求头

然后进行请求方法的封装，可以将 get、post、delete 等封装成对应的方法，便于使用

最后对请求拦截器和响应拦截器进行封装，添加 token、对返回码进行判断并相应，对 token 过期问题进行处理等等

#### vue-router

**传参**
params 传参
this.$router.push({name: '', params:{id: xxx}})
this.$route.params.id

props 解耦传参
在路由中开启 props，然后 path 中使用:id 的格式
组件内可以通过 props 的形式进行接受

query 传参
this.$router.push({ name:xxx, query:{ id: '' } })
this.$route.query.id

**hash 和 history 模式**

hash 的 url 中会带有#，history 中没有
history 会有历史记录
回车刷新时，hash 会重新加载页面，history 会报 404

一般会通过路由守卫对 hash 模式下路由变化进行监听，在组件内部也可以通过对$route 对象进行监听

**路由守卫**

是由 vue-router 提供的，在路由跳转前后执行逻辑，一般用来进行权限验证、用户信息验证、修改路由参数或者重定向，也可以通过在路由中添加属性判断是否进行路由拦截

**动态路由**

vue 中一般会在登录后获取用户信息，然后根据用户信息进行权限验证，获取对应的菜单列表
然后将菜单列表存入本地存储中，并在路由守卫里，通过 addRoute 方法进行动态路由添加

#### pinia

pinia 在刷新后会丢失数据，但是可以通过开启 persist 属性将数据存储到本地存储中，实现持久化存储

pinia 包含三个属性：state、getter、actions
分别是数据、数据的计算属性、对数据执行的操作
在 vue3 中，三个属性对应为 ref、computed 和 函数

一般会在多页面共享数据时进行使用，如用户信息、登录认证、购物车列表等等数据

#### 双向绑定

vue3 中采用了 proxy，替代了 vue2 中的 object.defineProperty()，解决了 vue2 无法监听数组索引变化等问题

在双向绑定过程中，主要包含三个过程：依赖收集、触发更新、批量更新
组件渲染时会触发 getter，vue 记录所有依赖于该数据的组件
数据修改时触发 setter，通知所有依赖的组件进行渲染
vue3 通过调度器进行批量更新，避免重复渲染

#### 组件封装

如果是全局组件，会将封装的组件放入 components 文件夹下，组件内部根据需求可以自定义 props、emits，或者通过 defineExpose 向组件的 ref 上添加属性和方法

如果想要将组件全局挂在，可以在 main.js 文件中通过 app.component 方法挂载，组件内使用只需要单独引入并使用就可以

vue 组件还支持数据的双向绑定、插槽、具名插槽等功能

#### Vue 强制刷新

this.$router.go(0)
localtion.reload()

#### vue3 和 vue2 的区别

数据双向绑定的实现原理不同
可以使用组合式 API，将相同功能的代码放在一起，便于维护开发
生命周期不同
