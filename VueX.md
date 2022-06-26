# VueX

## 什么状态需要我们在多个组件间共享的呢？

### 用户的登录状态，用户名称，头像，地理位置信息

### 商品的收藏，购物车中的物品

~~~js
./store

import Vue from 'vue'
import Vuex from 'vuex'
 // 1.安装插件
Vue.use(Vuex)
//2. 创建对象

const store = new Vuex.store({
    // 保存状态
    state: {
        counter:1000,       // 在其他组件中使用的时候就可以直接  <h2>{{$store.sate.counter}}</h2>
        students:[
            {age:20,name:'阿虎'},
            {age:8,name:'阿a'},
            
        ]
    },
    mutations:{
        // 监听同步state数据改动记录
        increment(state){                     // 在其他模板调用时 $states.commit('increment')
            state.count++
        },
        decrement(state){
            state.count--
        },										// 模板中想要改变store中的state数据方法
        // 方法一								 // addCount(count){
        decrementCount(sate,n){				  // 普通的提交方式this.$store.commit("invrementCount", count)}// 
            state.count -=n
                // 特殊的提交封装

        }，
        // 方法二
        decrementCount(state,payload){       //         // 特殊的提交封装   模板中想要改变store中的state数据方法
    													// addCount(count){
     	    state.counter -= payload.incrementCount;    //		this.$store.commit({
                                                        //      type:"incrementCount",
                                                        //      count
                                                        //})

            }
        
    },
    actions:{},
    // 类似于计算属性
    getters:{                           // 其他组件使用： <h2>{{$store.getters.powerCounter}}</h2>
        powerCounter(state){
            return state.counter**2
        },
        more20stu(state){					// 	<h2>{{$store.getters.more20stu}}</h2>
        	return state.students.filter(s=>s.age>20)    
		},
        moreAgeStu(state){					// 	<h2>{{$store.getters.moreAgeStu(18)}}</h2>
        	return function(age){
                return state.students.filter(s=> s.age >age)
            } 
		}
    },
    modules:{}
})

// 3.导出store独享
export default store



./main.js

import store from './store'
new Vue({
    el:'#app',
    store,              // 相当于 Vue.prototype.$store = store
    render: h=>h(App)
})
~~~





## state  --------> Vue Compontents ==> Actions ==> Mutations ==> states

​						模板展现                     改变state数据第一步，可以监听异步操作(后端api)            监听同步操作                  





## Mutation响应规则 -- 同步函数

### 当state中的数据发生改变时，Vue组件会自动更新

#### 当给state中对象添加新属性时，使用下面的方法：

方法一： 使用 Vue.set(obj, 'newProp', 12)

#### 当删除sate中元素

Vue.delete(state.info, 'age')







# Action ---- 异步操作

~~~js
actions:{									
    // context:上下文  store
    aUpdateInfo(context){
        setTimeout(()=>{
            context.commit('updateInfo')
        },1000)
    }
}


// 模板想调用aUpdateInfo
unpdateInfo(){
    this.$store.dispatch('aUpdateInfo')
}
~~~





## 或者使用Promise返回，用then调用，当异步改变state中值的时候做出提示

~~~js
actions:{									
    // context:上下文  store
    aUpdateInfo(context, payload){
      	return new Promise(resolve, reject)=>{
            setTimeout(()=>{
                context.commit('updateInfo');
                console.log(payload)
                resolve(payload)
                 
            },1000)
        }
    }
}


// 模板中调用方式

// 模板想调用aUpdateInfo
unpdateInfo(){
    this.$store.dispatch('aUpdateInfo'，"我已经完成修改操作").then((res)=>{
        console.log("里面完成了提交")
        console.log(res)
    })
}
~~~





# Module

~~~js
const moduleA = {
    state:{name: 'aj',}
    mutations:{
    	updateName(state,payload){
            state.name = payload
        }
	},
    actions:{
        aUpdateName(context){
            setTimeout(()=>{
                context.commit("updateName", "wangwu"
            }
        },
        // 或者可以这么写
        aUpdateName({state, commit, rootState}){   // es6语法，context由state ,commit, rootState构成
            setTimeout(()=>{
                commit("updateName", "wangwu"
            }
        },            
    },
    getters:{
    	fullName(state){
            return state.name + "111111
        },
        fullName2(state, getters){
            return getters.fullNmae + "2222"
        },
        fullName3(state, getters, tootState){
            return getters.fullName2 + rootState.nounter    // lisi11111122221000
        },
	}
const moduleB= {
    state:{},
    mutations:{},
    actions:{},
    getters:{}
},
const moduleC= {
    state:{},
    mutations:{},
    actions:{},
    getters:{}
}

const store = new Vuex.Store({
    state{
    	counter:1000
}
    modules{
    	a: moduleA,
    	B moduleAb
	}
})

store.state.a  // moduleA的状态
store.state.b// moduleB态


模板调用时候
<h2>{{$store.state.a.name}}</h2>
<button @click="updateName"  </button>
<h2>{{$store.getters.fullNmae}}</h2>
<button @click="asyncUpdateName"> 异步操作在action里面  </button>

updateName(){
    this.$store.commit("updateName", "lisi")
}，
asyncUpdateName(){
    this.$store.dispatch("aUpdateName")
}
~~~

