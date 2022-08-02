## 1.Vuex管理数据的属性有哪几个？作用是什么？

有五种,分别是State , Getter , Mutation , Action , Module (就是mapAction)

1. state：vuex的基本数据，用来存储变量
2. geeter：从基本数据(state)派生的数据，相当于state的计算属性
3. mutation：提交更新数据的方法，必须是同步的(如果需要异步使用action)。
   - 每个mutation 都有一个字符串的 事件类型 (type) 和 一个 回调函数 (handler)。
   - 回调函数就是我们实际进行状态更改的地方，并且它会接受 state 作为第一个参数，提交载荷作为第二个参数。
4. action：和mutation的功能大致相同，不同之处在于 ==>
   1. Action 提交的是 mutation，而不是直接变更状态。 
   2. Action 可以包含任意异步操作。
5. modules：模块化vuex，可以让每一个模块拥有自己的state、mutation、action、getters,使得结构非常清晰，方便管理。

## 2.axios有哪些特点？

Axios是一个基于promise的网络请求库，作用于node.js和服务器中

特点：

- 从浏览器创建XMLHttpRequests
- 从node.js创建http请求
- 支持Promise API
- 拦截请求和响应
- 转换请求和响应数据
- 取消请求
- 自动转换JSON数据
- 客户端支持防御XSRF
  - XSRF是什么？
    - XSRF是一种依赖web浏览器的、被混淆过的代理人攻击。
  - 防范措施
    - 严格过滤用户输入，慎重处理信息显示输出
    - GET方法只用于读取和显示数据
    - 在所有的POST数据中心添加一个“随机数”，通常这个被称之为Token

## 3.举列说明项目中src目录下6个常用的文件夹,他们的作用?

![src图讲解](https://chenwei-blog-1301583529.cos.ap-chengdu.myqcloud.com/src%E7%9B%AE%E5%BD%95%E6%AF%8F%E4%B8%AA%E6%96%87%E4%BB%B6%E5%A4%B9%E5%92%8C%E6%96%87%E4%BB%B6%E7%9A%84%E7%94%A8%E6%B3%95%E5%9B%BE.png)

1. assets 文件夹是放静态资源
2. components 文件夹是放全局组件的
3. router 文件夹是定义路由相关的配置
4. store 文件夹是管理 vuex管理数据的位置 模块化开发 全局getters
5. views 视图 所有页面 路由级别的组件
6. App.vue 入口页面 根组件
7. main.js 入口文件 加载组件 初始化等

### 3.1-拓展vue-admin-template的目录

![image-20220713210359843](https://chenwei-blog-1301583529.cos.ap-chengdu.myqcloud.com/vue-admin-template%E7%9B%AE%E5%BD%95.png)

~~~
├── build                      # 构建相关
├── mock                       # 项目mock 模拟数据，在接口服务器没有就绪时，临时充当接口
├── public                     # 静态资源
│   ├── favicon.ico            # favicon图标
│   └── index.html             # html模板
├── src                        # 源代码
│   ├── api                    # 所有请求
│   ├── assets                 # 主题 字体等静态资源  不会参与打包  直接直出
│   ├── components             # 全局公用组件 和业务不相关  上传组件
│   ├── icons                  # 项目所有 svg icons
│   ├── layout                 # 全局 layout 负责搭建项目的整体架子结构 html结构
│   ├── router                 # 路由
│   ├── store                  # 全局 store管理 vuex管理数据的位置 模块化开发 全局getters
│   ├── styles                 # 全局样式
│   ├── utils                  # 全局公用方法 request.js
│   ├── vendor                 # 公用vendor
│   ├── views                  # views 所有页面 路由级别的组件
│   ├── App.vue                # 入口页面 根组件
│   ├── main.js                # 入口文件 加载组件 初始化等
│   └── permission.js          # 权限管理
│   └── settings.js            # 配置文件
├── tests                      # 测试
├── .env.xxx                   # 环境变量配置
├── .eslintignore              # eslint 忽略文件
├── .eslintrc.js               # eslint 配置项
├── .gitignore                 # git 忽略文件
├── .travis.yml                # 自动化CI配置
├── .babel.config.js           # babel-loader 配置
├── jest.config.js             # 测试配置
├── vue.config.js              # vue-cli 配置
├── postcss.config.js          # postcss 配置
└── package.json               # package.json
~~~

## 4.Vue页面刷新的时候, 有些值会出现闪烁的情况,什么情况造成的?以及解决方案是什么?

在**`v-show设置隐藏元素`**是出现导致页面闪烁的问题

解决方案：

- **`v-cloak`** 解释--> v-cloak指令可以**`像CSS选择器一样绑定一套CSS样式然后这套CSS会一直生效到实例编译结束`**。
- **`v-text`** 解释--> vue中我们会将数据包在两个大括号中，然后放到HTML里，但是在vue内部，所有的双括号会被编译成textNode的一个v-text指令。所以使用v-text可以永远获得更好的性能，更重要的是可以避免FOUC

## 1.利用axios发送请求的时候，想一次发送5个请求，并且返回参数的顺序按照发送的顺序拿到，怎么做？

**`我知道你们想说通过不停.then的方式，我想听的是有没有更优雅的方式？`**

新的方法：

Promise.all([ajax1, ajax2, ajax3 ...]), 返回值 .then(res => res)也是一个数组,[ajax1的res, ajax2的res, ajax3的res...]

## 2.v-if 与 v-for 的优先级哪个高？

- 在vue2中，v-for的优先级高于v-if
- 在vue3中，v-if的优先级高于v-for
  - 两者用在一起会特别消耗性能
- 解决方案
  - 将**`v-if放在外层嵌套template`**（页面渲染不生成dom节点），在这一层进行v-if判断，然后在内部进行v-for循环
  - 如果条件出现在循环内部,不得不放在一起时,可通过计算属性computed提前过滤掉那些不需要显示的数据

## 3.vuex 和 localStorage 的区别是什么？

1. 最重要的区别：
   - vuex中的数据是**存储在内容中的，页面刷新会丢失**
   - localStorage**存在计算机本地，刷新并不会丢失**
     - sessionStorage生存于**应用会话之间**
2. 应用场景：
   - vuex用于组件之间的传值**(响应式的)**
   - localStorage主要用于不同页面之间的传值(其他页面更新数据了，当前页面要刷新才能相应更新，**非响应式的**)
3. 永久性：
   - vuex全局变量存储，当刷新页面时**vuex存储的值会丢失(内存中，必然丢失)，localStorage则不会**

## 4.谈一谈vue中的环境变量?

环境变量是什么？在一个产品的前端开发过程中，一般都会`经历本地开发、测试脚本、开发自测、测试环境、预上线环境`，然后才能正式的发布，对应每一个环境可能都会有所差异，所以我们要在各个环境切换的时候，需要不同的配置参数，就可以用环境变量和模式来方便我们管理。

**`process.env.NODE_ENV`** 是VUE-CLI脚手架自带的环境变量，依赖于项目的启动命令，自动切换开发环境
环境变量保存的值： **`development--开发环境   test--测试环境   production--生产环境`**

配置文件:  .env.development-->开发环境会被加载   .env.production-->生产环境会被加载
在配置文件中写 键 = 值 的写法  获取方式：process.env.键

## 1.谈谈vue-router的几个钩子函数 ,以及触发时机?

#### **1、全局守卫**

**定义在全局，定义在路由中，进入任意一个路由都会调用）**

##### （1）**beforeEach  全局前置守卫**

`beforeEach`在每一次导航之前都会触发，此时的`to`指的是将要跳转到的路由地址，`from`指的是从哪一个路由地址跳转的，`next`表示跳转方法。                                                                                                                                                              通常做的就是在这里验证是否登录,没有登录就返回. 

```js
router.beforeEach((to, from, next) => {
console.log(to)
  console.log(from)
  next()
})
```

**参数：**

`beforeEach` 全局前置守卫接收三个参数

- to: 即将要进入的目标路由对象
- from: 当前导航正要离开的路由对象
- next:  一定要调用该方法不然会阻塞路由。

**注意：** `next` 参数可以不添加，但是一旦添加，则必须调用一次，否则路由跳转等会停止。

`next（）`方法的几种情况

- **next():** 进行管道中的下一个钩子。
- **next(false):** 中断当前的导航。回到 `from` 路由对应的地址。
- **next(’/’) 或者 next({ path: ‘/’ }):** 跳转到一个不同的地址，可传递的参数与 `router.push` 中选项一致。
- **next(error):** 导航终止，且该错误会被传递给 `router.onError()` 注册过的回调。

全局前置守卫可以定义多个，根据创建顺序调用。在所有守卫完成之前导航一直处于等待中。 

##### **（2）**beforeResolve 全局解析守卫(同样有3个参数)

全局解析守卫，在路由跳转前，所有 **组件内守卫** 和 **异步路由组件** 被解析之后触发，它同样在 **每次导航** 时都会触发。 

**（3）afterEach全局后置守卫**

全局后置钩子，它发生在路由跳转完成后，`beforeEach` 和 `beforeResolve` 之后，`beforeRouteEnter`（组件内守卫）之前。它同样在 **每次导航** 时都会触发。 

这个钩子的两个参数和 `beforeEach` 中的 `to` 和 `from` 一样。然而和其它全局钩子不同的是，这些钩子不会接受 `next` 函数，也不会改变导航本身。 

#### 2、单独路由独享组件

**只要用于指定某个特定路由跳转时的逻辑,写在某个路由配置内部**

- beforeEnter：进入该路由之前             参数包括 `to`，`from`，`next`。                                                                                                                      需要在路由配置上定义 `beforeEnter` 守卫，此守卫只在进入路由时触发，在 `beforeEach` 之后紧随执行，不会在 `params`、`query` 或 `hash` 改变时触发。 

```js
const router = new VueRouter({
  routes: [
    {
      path: '/foo',
      component: Foo,
      beforeEnter: (to, from, next) => {
        // ...
      }
    }
  ]
})
```

#### **3、组件内钩子** 

**定义在路由组件内部的守卫。**

- beforeRouteEnter：进入组件时   参数包括 `to`，`from`，`next`。 

  该钩子在全局守卫 `beforeEach` 和路由守卫 `beforeEnter` 之后，全局 `beforeResolve` 和全局 `afterEach` 之前调用。                                                                                                                                                                                       该守卫内访问不到组件的实例，也就是 `this` 为 `undefined`，也就是他在 `beforeCreate` 生命周期前触发。 

- beforeRouteUpdate：路由不变，传递的参数改变,参数包括 `to`，`from`，`next`

  当组件没有经历创建和销毁,仅仅是路由参数有更新的时候执行该函数 ,可以访问this

- beforeRouteLeave： 离开组件前,参数包括 `to`，`from`，`next`    可以访问this

```js
const UserDetails = {
  template: `...`,
  beforeRouteEnter(to, from) {
    // 在渲染该组件的对应路由被验证前调用
    // 不能获取组件实例 `this` ！
    // 因为当守卫执行时，组件实例还没被创建！
  },
  beforeRouteUpdate(to, from) {
    // 在当前路由改变，但是该组件被复用时调用
    // 举例来说，对于一个带有动态参数的路径 `/users/:id`，在 `/users/1` 和 `/users/2` 之间跳转的时候，
    // 由于会渲染同样的 `UserDetails` 组件，因此组件实例会被复用。而这个钩子就会在这个情况下被调用。
    // 因为在这种情况发生的时候，组件已经挂载好了，导航守卫可以访问组件实例 `this`
  },
  beforeRouteLeave(to, from) {
    // 在导航离开渲染该组件的对应路由时调用
    // 与 `beforeRouteUpdate` 一样，它可以访问组件实例 `this`
  },
}
```

完整的导航解析流程

1. 导航被触发。
2. 在失活的组件里调用 `beforeRouteLeave` 守卫。
3. 调用全局的 `beforeEach` 守卫。
4. 在重用的组件里调用 `beforeRouteUpdate` 守卫。
5. 在路由配置里调用 `beforeEnter`。
6. 解析异步路由组件。
7. 在被激活的组件里调用 `beforeRouteEnter`。
8. 调用全局的 `beforeResolve` 守卫。
9. 导航被确认。
10. 调用全局的 `afterEach` 钩子。
11. 触发 `DOM` 更新。
12. 调用 `beforeRouteEnter` 守卫中传给 `next` 的回调函数，创建好的组件实例会作为回调函数的参数传入。

完整的导航解析流程

1. 导航被触发。
2. 在失活的组件里调用 `beforeRouteLeave` 守卫。
3. 调用全局的 `beforeEach` 守卫。
4. 在重用的组件里调用 `beforeRouteUpdate` 守卫。
5. 在路由配置里调用 `beforeEnter`。
6. 解析异步路由组件。
7. 在被激活的组件里调用 `beforeRouteEnter`。
8. 调用全局的 `beforeResolve` 守卫。
9. 导航被确认。
10. 调用全局的 `afterEach` 钩子。
11. 触发 `DOM` 更新。
12. 调用 `beforeRouteEnter` 守卫中传给 `next` 的回调函数，创建好的组件实例会作为回调函数的参数传入。

## 2.路由配置中常用的属性及作用,至少5个?

路由配置参数：

- path : 跳转路径
- component : 路径相对于的组件
- name:命名路由
- children:子路由的配置参数(路由嵌套)
- props:路由解耦
- redirect : 重定向路由           

## 3.active-class 是哪个组件的属性？

active-class是**vue-router模块的router-link组件中的属性**，用来做**`选中样式的切换`**

在vue-router中使用的方法有两种：

1. 在router-link中写入

   - 在选择样式时根据路由中的路径(to=“/home”）去匹配，然后显示

   - ~~~javascript
       <router-link to="/home" active-class ="active">首页
       </router-link>
     ~~~

2. 直接在路由 js 文件中配置  linkActiveClass

   - ~~~javascript
     export default new Router({
     linkActiveClass: 'active',
     })
     ~~~

## 4.vue-router响应路由参数的变化？

**例：例如从 /user/aside导航到 /user/foo, 加载的都是/user对应的组件,/aside和/foo是传递的动态参数. 就是同一个组件跳到同一个组件,组件的生命周期钩子函数不会触发, 现在传递了不同的参数, `怎么样才能触发加载后端数据的函数呢`?**

第一种：组件内的钩子函数  beforerouteupdate()

~~~vue
 beforeRouteUpdate (to, from, next) {
   
 }
~~~

第二种：可以**`watch (监测变化) $route 对象`** 

~~~javascript
watch: {
    '$route' (to, from) {
      // 对路由变化作出响应...
}
~~~

第三种：在父组件的router-view上加个key 

~~~javascript
<router-view :key="$route.fullPath"></router-view>
~~~

