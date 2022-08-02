## 1.什么是动态组件?如何使用？

动态组件指的是: **`动态切换组件的显示与隐藏`**

使用：

1. **`<component>`** 是组件的 **`占位符`**
2. 通过 **`is属性`** 动态指定要渲染的组件名称
3. ~~eg: <component is = “要渲染组件的名称"></component>~~

## 2.如何进行组件缓存?有什么好处？如何知道缓存的组件是出现还是消失了?

通过对列表组件使用keep-alive进行缓存，并且可以设置标签include和exclude属性缓存一个或多个组件

数据的读取速度是非常快的，能大量减少对数据库的访问，减少数据库的压力。

**`include`** 和 **`exclude`** 的区别是前者是只有名称匹配的组件才会缓存，后者是相反的，是任何名称匹配的组件不会被缓存

## 3.谈谈组件插槽，怎么用？

props允许父组件传递数据，插槽允许父组件传递标签

1. 默认插槽：
   - 在子组件用slot占位，在父组件向子组件内添加标签，就实现默认插槽
2. 具名插槽：
   - 组件内有多个插槽的时候，使用具名插槽， **`在子组件的插槽中给slot添加name属性`** ，在父组件需要使用插槽的地方，用slot添加名称 
3. 作用域插槽：
   - 子组件往父组件传值，定义一个属性名+数据传到父组件，在父组件的template模板用v-slot接收，如果不使用template模板，就使用slot-scope接收

## 4.Vue有哪些常用的指令(说5个)？自定义指令怎么用?自定义指令你在项目中使用过的场景?

1. v-model:多用于**表单元素实现双向数据绑定**
2. v-for:对**数组的选项列表进行渲染**
3. v-show:显示内容(对元素的隐藏-不销毁元素)
4. v-hide:隐藏内容
5. v-if:显示与隐藏(dom元素的删除添加)
6. v-else-if/v-else:必须和v-if连用，否则会模板编译错误
7. v-bind:动态绑定
8. v-on:click:给标签绑定函数，可以简写成@，绑定函数必须卸载methods里
9. v-text:解析文本
10. v-html：解析浏览器
11. v-once:进入页面时，只渲染一次，不在进行渲染
12. v-clock:防止闪烁
13. v-pre:把标签内部的元素原位输出



全局定义指令: **`Vue.directive(‘指令名称’，函数)`**

~~`~~Vue.directive`第一个参数是指令的名字（不需要写上`v-`前缀），第二个参数可以是对象数据，也可以是一个指令函数~~~~

~~~javascript
// 注册一个全局自定义指令 `v-focus`
Vue.directive('focus', {
  // 当被绑定的元素插入到 DOM 中时……
  inserted: function (el) {
    // 聚焦元素
    el.focus()  // 页面加载完成之后自动让输入框获取到焦点的小功能
  }
})
~~~

局部注册通过在组件`options`选项中设置`directive`属性

~~~JavaScript
directives: {
  focus: {
    // 指令的定义
    inserted: function (el) {
      el.focus() // 页面加载完成之后自动让输入框获取到焦点的小功能
    }
  }
}
~~~

~~在模板中任何元素上使用新的 `v-focus` property，如下：~~

~~~JavaScript
<input v-focus />
~~~

组件内定义指令: **`directives` 钩子函数**

-  **`bind:只调用一次，指令第一次绑定到元素时调用`** 。在这里可以进行一次性的初始化设置
-  inseted:被绑定元素插入父节点时调用(仅保存父节点存在，但不一定已被插入到文档中)
-  update:所在模板被重新解析时

自定义指令的应用场景：

- 表单防止重复提交

  - ~~~JavaScript
    // 1.设置v-throttle自定义指令
    Vue.directive('throttle', {
      bind: (el, binding) => {
        let throttleTime = binding.value; // 节流时间
        if (!throttleTime) { // 用户若不设置节流时间，则默认2s
          throttleTime = 2000;
        }
        let cbFun;
        el.addEventListener('click', event => {
          if (!cbFun) { // 第一次执行
            cbFun = setTimeout(() => {
              cbFun = null;
            }, throttleTime);
          } else {
            event && event.stopImmediatePropagation();
          }
        }, true);
      },
    });
    // 2.为button标签设置v-throttle自定义指令
    <button @click="sayHello" v-throttle>提交</button>
    ~~~

- 图片懒加载

  - ~~~JavaScript
    const LazyLoad = {
        // install方法
        install(Vue,options){
        	  // 代替图片的loading图
            let defaultSrc = options.default;
            Vue.directive('lazy',{
                bind(el,binding){
                    LazyLoad.init(el,binding.value,defaultSrc);
                },
                inserted(el){
                    // 兼容处理
                    if('IntersectionObserver' in window){
                        LazyLoad.observe(el);
                    }else{
                        LazyLoad.listenerScroll(el);
                    }
                    
                },
            })
        },
        // 初始化
        init(el,val,def){
            // data-src 储存真实src
            el.setAttribute('data-src',val);
            // 设置src为loading图
            el.setAttribute('src',def);
        },
        // 利用IntersectionObserver监听el
        observe(el){
            let io = new IntersectionObserver(entries => {
                let realSrc = el.dataset.src;
                if(entries[0].isIntersecting){
                    if(realSrc){
                        el.src = realSrc;
                        el.removeAttribute('data-src');
                    }
                }
            });
            io.observe(el);
        },
        // 监听scroll事件
        listenerScroll(el){
            let handler = LazyLoad.throttle(LazyLoad.load,300);
            LazyLoad.load(el);
            window.addEventListener('scroll',() => {
                handler(el);
            });
        },
        // 加载真实图片
        load(el){
            let windowHeight = document.documentElement.clientHeight
            let elTop = el.getBoundingClientRect().top;
            let elBtm = el.getBoundingClientRect().bottom;
            let realSrc = el.dataset.src;
            if(elTop - windowHeight<0&&elBtm > 0){
                if(realSrc){
                    el.src = realSrc;
                    el.removeAttribute('data-src');
                }
            }
        },
        // 节流
        throttle(fn,delay){
            let timer; 
            let prevTime;
            return function(...args){
                let currTime = Date.now();
                let context = this;
                if(!prevTime) prevTime = currTime;
                clearTimeout(timer);
                
                if(currTime - prevTime > delay){
                    prevTime = currTime;
                    fn.apply(context,args);
                    clearTimeout(timer);
                    return;
                }
    
                timer = setTimeout(function(){
                    prevTime = Date.now();
                    timer = null;
                    fn.apply(context,args);
                },delay);
            }
        }
    
    }
    export default LazyLoad;
    ~~~

- ~~一键 Copy的功能~~

  - ~~~javascript
    import { Message } from 'ant-design-vue';
    
    const vCopy = { //
      /*
        bind 钩子函数，第一次绑定时调用，可以在这里做初始化设置
        el: 作用的 dom 对象
        value: 传给指令的值，也就是我们要 copy 的值
      */
      bind(el, { value }) {
        el.$value = value; // 用一个全局属性来存传进来的值，因为这个值在别的钩子函数里还会用到
        el.handler = () => {
          if (!el.$value) {
          // 值为空的时候，给出提示，我这里的提示是用的 ant-design-vue 的提示，你们随意
            Message.warning('无复制内容');
            return;
          }
          // 动态创建 textarea 标签
          const textarea = document.createElement('textarea');
          // 将该 textarea 设为 readonly 防止 iOS 下自动唤起键盘，同时将 textarea 移出可视区域
          textarea.readOnly = 'readonly';
          textarea.style.position = 'absolute';
          textarea.style.left = '-9999px';
          // 将要 copy 的值赋给 textarea 标签的 value 属性
          textarea.value = el.$value;
          // 将 textarea 插入到 body 中
          document.body.appendChild(textarea);
          // 选中值并复制
          textarea.select();
          // textarea.setSelectionRange(0, textarea.value.length);
          const result = document.execCommand('Copy');
          if (result) {
            Message.success('复制成功');
          }
          document.body.removeChild(textarea);
        };
        // 绑定点击事件，就是所谓的一键 copy 啦
        el.addEventListener('click', el.handler);
      },
      // 当传进来的值更新的时候触发
      componentUpdated(el, { value }) {
        el.$value = value;
      },
      // 指令与元素解绑的时候，移除事件绑定
      unbind(el) {
        el.removeEventListener('click', el.handler);
      },
    };
    
    export default vCopy;
    ~~~

~~自定义指令还有很多应用场景，如：拖拽指令、页面水印、权限校验等等应用场景~~