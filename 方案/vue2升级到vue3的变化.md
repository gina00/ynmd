# vue2升级到vue3的变化
- [Vue3的优点](#vue3的优点)
- [生命周期](#生命周期)
- [组合式API和setup语法糖](#组合式API和setup语法糖)
- [响应式原理ref和reactive](#响应式原理ref和reactive)
- [computed和watch](#computed和watch)
- [组件通信](#组件通信)
- [v-model和sync](#v-model和sync)
- [路由](#路由)
- [技术栈](#技术栈)

## vue3的优点
### 增加了代码的可维护性
1. Vue2 使用的是 options 的API ，代码逻辑比较分散，可读性差，可维护性差。
2. Vue3 使用的是 compositionAPI 逻辑分明，可维护性高，更友好的支持TS。在 template 模板中支持多个根节点，支持jsx语法。
### 提升了页面渲染性能
1. 在 Vue2 中,每次更新diff，都是全量对比。
2. Vue3 在更新DOM算法上，做了优化。只对比带有标记的，这样大大减少了非动态内容的对比消耗。
### 加强了 MVVM 双向数据绑定的效率
   Vue2 的双向数据绑定是利用 ES5 的 Object.definePropert() 对对象属性进行劫持，结合 发布订阅模式的方式来实现的。
   1. Vue3 中使用了 es6 的 ProxyAPI 对数据代理。
   2. 相比于vue2.x，使用proxy的优势如下：
    (1). defineProperty只能监听某个属性，不能对全对象监听
    (2). 可以省去for in、闭包等内容来提升效率（直接绑定整个对象即可）
    (3). 可以监听数组，不用再去单独的对数组做特异性操作 vue3.x 可以检测到数组内部数据的变化

## 生命周期
### Vue2和Vue3生命周期的差异
Vue2(选项式)|Vue3(组合式)|描述
:---|:---|:---
beforeCreate|使用 setup()|组件实例初始化完成之后立即调用
created|使用 setup()|组件实例处理完所有与状态相关的选项后调用，挂载未开始
beforeMount|onBeforeMount|组件被挂载之前调用，还未执行 DOM 渲染过程
mounted|onMounted|组件被挂载之后调用，完成了DOM渲染
beforeUpdate|onBeforeUpdate|组件即将因为一个响应式状态变更而更新其 DOM 树之前调用
updated|onUpdated|组件因为一个响应式状态变更而更新其 DOM 树之后调用
beforeUnmount|onBeforeUnmount|在一个组件实例被卸载之前调用
unmounted |onUnmounted|在一个组件实例被卸载之后调用

区别：beforeCreate与created并没有组合式API中,setup就相当于这两个生命周期函数

## 组合式API和setup语法糖
Vue3.0给我们提供了composition API，而实现composition API这种代码风格主要是使用官方提供的setup这个函数。
首先实现一个同样的逻辑(点击切换页面数据)看一下它们直接的区别

**选项式Api**
``` js
<template>
  <div @click="changeMsg">{{msg}}</div>
</template>
<script>
export default  {
  data(){
    return {
     msg:'hello world'
    }
  },
  methods:{
    changeMsg(){
      this.msg = 'hello juejin'
    }
  }
}
</script>

```
**组合式API**
```js
<template>
 <div @click="changeMsg">{{msg}}</div>
</template>

<script>
import { ref,defineComponent } from "vue";
export default defineComponent({
setup() {
    const msg = ref('hello world')
    const changeMsg = ()=>{
      msg.value = 'hello juejin'
    }
return {
  msg,
  changeMsg
};
},
});
</script>
```
**setup 语法糖**
```js
<template>
  <div @click="changeMsg">{{ msg }}</div>
</template>

<script setup>
import { ref } from "vue";

const msg = ref('hello world')
const changeMsg = () => {
  msg.value = 'hello juejin'
}
</script>
```
**总结**

选项式Api是将data和methods包括后面的watch，computed等分开管理，而组合式Api则是将相关逻辑放到了一起（类似于原生js开发）。
setup语法糖则可以让变量方法不用再写return，后面的组件甚至是自定义指令也可以在template中自动获得。



## 响应式原理ref和reactive
在组合式api中，data函数中的数据都具有响应式，页面会随着data中的数据变化而变化，而组合式api中不存在data函数该如何呢？所以为了解决这个问题Vue3引入了ref和reactive函数来将使得变量成为响应式的数据。

**组合式Api**
```js
<script>
import { ref,reactive,defineComponent } from "vue";
export default defineComponent({
setup() {
let msg = ref('hello world')
let obj = reactive({
    name:'juejin',
    age:3
})
const changeData = () => {
  msg.value = 'hello juejin'
  obj.name = 'hello world'
}
return {
msg,
obj,
changeData
};
},
});
</script>
```
**setup语法糖**
```js
<script setup>
import { ref,reactive } from "vue";
let msg = ref('hello world')
let obj = reactive({
    name:'juejin',
    age:3
})
const changeData = () => {
  msg.value = 'hello juejin'
  obj.name = 'hello world'
}
</script>
```

### ref
作用：定义一个响应式的数据，或者说是生成一个引用实现对象
语法：const xxx = ref(initValue)
1. 创建一个包含响应式数据的引用对象（reference对象）
2. JS中操作数据需要：xxx.value
3. 模板中读取数据：直接使用即可

ref接收的数据可以是基本类型数据，也可以是对象类型
基本类型的数据：响应式是靠Object.defineProperty()的get和set完成的
对象类型的数据：内部使用了reactive函数

### reactive 
作用：定义一个对象类型的响应式数据。
语法：const 代理对象 = reactive(源对象) 
1. 参数是一个对象或者数组，返回一个代理对象（Proxy的实例对象，简称proxy对象）。
2. reactive定义的响应式数据是深层次的。
3. 内部基于ES6的Proxy实现，通过代理对象操作源对象内部数据。
```js
<template>
  <div>
    <p>{{ user.name }}</p>
    <p>{{ user.age }}</p>
    <p>{{ user.country }}</p>
  </div>
</template>

<script setup lang="ts">
  import { reactive } from "@vue/reactivity";

  let user = reactive({
    name: "Yancy Zhang",
    age: 20,
    country: "China",
  });

  setTimeout(() => {
    user.age++;
  }, 1000);
</script>

<style scoped></style>

```
1. 若要避免深层响应式转换，只想保留对这个对象顶层次访问的响应性，请使用 shallowReactive() 作替代。
2. 不能通过 …state （扩展运算符）方式结构，这样会丢失响应式。
3. 注意reactive封装的响应式对象，不要通过解构的方式返回，这是不具有响应式的。可以通过 toRefs 处理，然后再解构返回，这样才具有响应式。
```js
const state = reactive({
  foo: 1,
  bar: 2
})

// state.foo 本来是一个响应式对象，被重新赋值后就不是响应式对象了，只是一个普通基本类型值

const {foo, bar} = state; // 此时 foo 就等于 1 了，1 是一个值，不是一个响应式对象
foo = 6; // 更改在视图中并不会生效，因为解构时 foo 被重新赋值了，即 const foo = state.foo; const foo = 1;

```
### toRef
基于响应式对象上的一个属性，创建一个对应的 ref。这样创建的 ref 与其源属性保持同步：改变源属性的值将更新 ref 的值，反之亦然。
```js
const state = reactive({
  foo: 1,
  bar: 2
})

const fooRef = toRef(state, 'foo')

// 更改该 ref 会更新源属性
fooRef.value++
console.log(state.foo) // 2

// 更改源属性也会更新该 ref
state.foo++
console.log(fooRef.value) // 3

```
### toRefs
将一个响应式对象转换为一个普通对象，这个普通对象的每个属性都是指向源对象相应属性的 ref。每个单独的 ref 都是使用 toRef() 创建的。
当从组合式函数中返回响应式对象时，toRefs 相当有用。使用它，消费者组件可以解构/展开返回的对象而不会失去响应性:
```js
function useFeatureX() {
  const state = reactive({
    foo: 1,
    bar: 2
  })

  // ...基于状态的操作逻辑

  // 在返回时都转为 ref
  return toRefs(state)
}

// 可以解构而不会失去响应性，因为解构后的 foo 是个 Ref 对象，如果直接解构state的话解构完是一个值 ‘1’
const { foo, bar } = useFeatureX()

```



**总结**

使用ref的时候在js中取值的时候需要加上.value。
reactive更推荐去定义复杂的数据类型 
ref 更推荐定义基本类型

## computed和watch

在vue2的选项式API中，可以在computed:{}和watch:{}中定义对应的计算属性和监听器。

### 选项式API
```js
<template>
  <div>{{ addSum }}</div>
</template>
<script>
export default {
  data() {
    return {
      a: 1,
      b: 2
    }
  },
  computed: {
    addSum() {
      return this.a + this.b
    }
  },
  watch:{
    a(newValue, oldValue){
      console.log(`a从${oldValue}变成了${newValue}`)
    }
  }
}
</script>
```
**组合式Api**
```js
<template>
  <div>{{addSum}}</div>
</template>
<script>
import { computed, ref, watch, defineComponent } from "vue";
export default defineComponent({
  setup() {
    const a = ref(1)
    const b = ref(2)
    let addSum = computed(() => {
      return a.value+b.value
    })
    watch(a, (newValue, oldValue) => {
     console.log(`a从${oldValue}变成了${newValue}`)
    })
    return {
      addSum
    };
  },
});
</script>
```
### setup语法糖
```js
<template>
  <div>{{ addSum }}</div>
</template>
<script setup>
import { computed, ref, watch } from "vue";
const a = ref(1)
const b = ref(2)
let addSum = computed(() => {
  return a.value + b.value
})
watch(a, (newValue, oldValue) => {
  console.log(`a从${oldValue}变成了${newValue}`)
})
</script>
```
Vue3中除了watch，还引入了副作用监听函数watchEffect，它和React中的useEffect很像，只不过watchEffect不需要传入依赖项。

#### 什么是watchEffect
watchEffect它会立即执行传入的一个函数，同时响应式追踪其依赖，并在其依赖变更时重新运行该函数。
```js
<template>
  <div>{{ watchTarget }}</div>
</template>
<script setup>
import { watchEffect,ref } from "vue";
const watchTarget = ref(0)
watchEffect(()=>{
  console.log(watchTarget.value)
})
setInterval(()=>{
  watchTarget.value++
},1000)
</script>
```
首先刚进入页面就会执行watchEffect中的函数打印出:0,随着定时器的运行，watchEffect监听到依赖数据的变化回调函数每隔一秒就会执行一次

<b>总结</b>

computed和watch所依赖的数据必须是响应式的。Vue3引入了watchEffect,watchEffect 相当于将 watch 的依赖源和回调函数合并，当任何你有用到的响应式依赖更新时，该回调函数便会重新执行。不同于 watch的是watchEffect的回调函数会被立即执行，即（{ immediate: true }）

## 组件通信
Vue中组件通信方式有很多，其中选项式API和组合式API实现起来会有很多差异；这里将介绍如下组件通信方式：

方式|Vue2|Vue3
:---|:--|:---
父传子|props|props
子传父|$emit|emits
父传子|$attrs$|attrs
子传父|$listeners|无(合并到attrs方式)
父传子|provide|provide
子传父|inject|inject
子组件访问父组件|$parent|无
父组件访问子组件|$children|无
父组件访问子组件|$ref|expose&ref


### props
props是组件通信中最常用的通信方式之一。父组件通过v-bind传入，子组件通过props接收，下面是它的三种实现方式

**选项式API**
```js
//父组件
<template>
  <div>
    <Child :msg="parentMsg" />
  </div>
</template>
<script>
  import Child from './Child'
  export default {
    components:{
      Child
    },
    data() {
      return {
        parentMsg: '父组件信息'
      }
    }
  }
</script>

//子组件
<template>
  <div>
    {{msg}}
  </div>
</template>
<script>
  export default {
    props:['msg']
  }
</script>
```
**组合式API**
```js
//父组件
<template>
  <div>
    <Child :msg="parentMsg" />
  </div>
</template>
<script>
  import { ref,defineComponent } from 'vue'
  import Child from './Child.vue'
  export default defineComponent({
    components:{
      Child
   },
   setup() {
     const parentMsg = ref('父组件信息')
      return {
        parentMsg
      };
    },
   });
</script>

//子组件
<template>
    <div>
        {{ parentMsg }}
    </div>
</template>
<script>
import { defineComponent,toRef } from "vue";
export default defineComponent({
    props: ["msg"],// 如果这行不写，下面就接收不到
    setup(props) {
        console.log(props.msg) //父组件信息
        let parentMsg = toRef(props, 'msg')
        return {
            parentMsg
        };
    },
});
</script>
```
**setup语法糖**
```js
//父组件
<template>
  <div>
    <Child :msg="parentMsg" />
  </div>
</template>
<script setup>
  import { ref } from 'vue'
  import Child from './Child.vue'
  const parentMsg = ref('父组件信息')
</script>

//子组件
<template>
    <div>
        {{ parentMsg }}
    </div>
</template>
<script setup>
  import { toRef, defineProps } from "vue";
  const props = defineProps(["msg"]);
  console.log(props.msg) //父组件信息
  let parentMsg = toRef(props, 'msg')
</script>
```
props中数据流是单项的，即子组件不可改变父组件传来的值

在组合式API中，如果想在子组件中用其它变量接收props的值时需要使用toRef将props中的属性转为响应式。
### emit
子组件可以通过emit发布一个事件并传递一些参数，父组件通过v-onj进行这个事件的监听

**选项式API**
```jsx
<template>
  <div>
    <Child @sendMsg="getFromChild" />
  </div>
</template>
<script>
  import Child from './Child'
  export default {
    components:{
      Child
    },
    methods: {
      getFromChild(val) {
        console.log(val) //我是子组件数据
      }
    }
  }
</script>

// 子组件
<template>
  <div>
    <button @click="sendFun">send</button>
  </div>
</template>
<script>
  export default {
    methods:{
      sendFun(){
        this.$emit('sendMsg','我是子组件数据')
      }
    }
  }
</script>
```
**组合式Api**
```jsx
//父组件
<template>
  <div>
    <Child @sendMsg="getFromChild" />
  </div>
</template>
<script>
  import Child from './Child'
  import { defineComponent } from "vue";
  export default defineComponent({
    components: {
      Child
    },
    setup() {
      const getFromChild = (val) => {
        console.log(val) //我是子组件数据
      }
      return {
        getFromChild
      };
    },
  });
</script>

//子组件
<template>
    <div>
        <button @click="sendFun">send</button>
    </div>
</template>

<script>
  import { defineComponent } from "vue";
  export default defineComponent({
      emits: ['sendMsg'],
      setup(props, ctx) {
          const sendFun = () => {
              ctx.emit('sendMsg', '我是子组件数据')
          }
          return {
              sendFun
          };
      },
  });
</script>
```
**setup语法糖**
``` js
//父组件
<template>
  <div>
    <Child @sendMsg="getFromChild" />
  </div>
</template>
<script setup>
  import Child from './Child'
  const getFromChild = (val) => {
      console.log(val) //我是子组件数据
    }
</script>

//子组件
<template>
    <div>
        <button @click="sendFun">send</button>
    </div>
</template>
<script setup>
  import { defineEmits } from "vue";
  const emits = defineEmits(['sendMsg'])
  const sendFun = () => {
      emits('sendMsg', '我是子组件数据')
  }
</script>
```
### attrs和listeners
子组件使用$attrs可以获得父组件除了props传递的属性和特性绑定属性 (class和 style)之外的所有属性。

子组件使用$listeners可以获得父组件(不含.native修饰器的)所有v-on事件监听器，在Vue3中已经不再使用；但是Vue3中的attrs不仅可以获得父组件传来的属性也可以获得父组件v-on事件监听器
**选项式API**
```js
//父组件
<template>
  <div>
    <Child @parentFun="parentFun" :msg1="msg1" :msg2="msg2"  />
  </div>
</template>
<script>
import Child from './Child'
export default {
  components:{
    Child
  },
  data(){
    return {
      msg1:'子组件msg1',
      msg2:'子组件msg2'
    }
  },
  methods: {
    parentFun(val) {
      console.log(`父组件方法被调用,获得子组件传值：${val}`)
    }
  }
}
</script>

//子组件
<template>
  <div>
    <button @click="getParentFun">调用父组件方法</button>
  </div>
</template>
<script>
export default {
  methods:{
    getParentFun(){
      this.$listeners.parentFun('我是子组件数据')
    }
  },
  created(){
    //获取父组件中所有绑定属性
    console.log(this.$attrs)  //{"msg1": "子组件msg1","msg2": "子组件msg2"}
    //获取父组件中所有绑定方法    
    console.log(this.$listeners) //{parentFun:f}
  }
}
</script>
```
**组合式API**
```js
//父组件
<template>
  <div>
    <Child @parentFun="parentFun" :msg1="msg1" :msg2="msg2" />
  </div>
</template>
<script>
import Child from './Child'
import { defineComponent,ref } from "vue";
export default defineComponent({
  components: {
    Child
  },
  setup() {
    const msg1 = ref('子组件msg1')
    const msg2 = ref('子组件msg2')
    const parentFun = (val) => {
      console.log(`父组件方法被调用,获得子组件传值：${val}`)
    }
    return {
      parentFun,
      msg1,
      msg2
    };
  },
});
</script>

//子组件

<template>
    <div>
        <button @click="getParentFun">调用父组件方法</button>
    </div>
</template>
<script>
import { defineComponent } from "vue";
export default defineComponent({
    emits: ['sendMsg'],
    setup(props, ctx) {
        //获取父组件方法和事件
        console.log(ctx.attrs) //Proxy {"msg1": "子组件msg1","msg2": "子组件msg2"}
        const getParentFun = () => {
            //调用父组件方法
            ctx.attrs.onParentFun('我是子组件数据')
        }
        return {
            getParentFun
        };
    },
});
</script>
```
**setup语法糖**
```js
//父组件
<template>
  <div>
    <Child @parentFun="parentFun" :msg1="msg1" :msg2="msg2" />
  </div>
</template>
<script setup>
import Child from './Child'
import { ref } from "vue";
const msg1 = ref('子组件msg1')
const msg2 = ref('子组件msg2')
const parentFun = (val) => {
  console.log(`父组件方法被调用,获得子组件传值：${val}`)
}
</script>

//子组件
<template>
    <div>
        <button @click="getParentFun">调用父组件方法</button>
    </div>
</template>
<script setup>
import { useAttrs } from "vue";
const attrs = useAttrs()
//获取父组件方法和事件
console.log(attrs) //Proxy {"msg1": "子组件msg1","msg2": "子组件msg2"}
const getParentFun = () => {
    //调用父组件方法
    attrs.onParentFun('我是子组件数据')
}
</script>
```
Vue3中使用attrs调用父组件方法时，方法前需要加上on；如parentFun->onParentFun
### provide/inject
provide：是一个对象，或者是一个返回对象的函数。里面包含要给子孙后代属性

inject：一个字符串数组，或者是一个对象。获取父组件或更高层次的组件provide的值，既在任何后代组件都可以通过inject获得

**选项式API**
```js
//父组件
<script>
import Child from './Child'
export default {
  components: {
    Child
  },
  data() {
    return {
      msg1: '子组件msg1',
      msg2: '子组件msg2'
    }
  },
  provide() {
    return {
      msg1: this.msg1,
      msg2: this.msg2
    }
  }
}
</script>

//子组件
<script>
export default {
  inject:['msg1','msg2'],
  created(){
    //获取高层级提供的属性
    console.log(this.msg1) //子组件msg1
    console.log(this.msg2) //子组件msg2
  }
}
</script>
```
**组合式API**
```js
//父组件
<script>
import Child from './Child'
import { ref, defineComponent,provide } from "vue";
export default defineComponent({
  components:{
    Child
  },
  setup() {
    const msg1 = ref('子组件msg1')
    const msg2 = ref('子组件msg2')
    provide("msg1", msg1)
    provide("msg2", msg2)
    return {
      
    }
  },
});
</script>

//子组件
<template>
    <div>
        <button @click="getParentFun">调用父组件方法</button>
    </div>
</template>
<script>
import { inject, defineComponent } from "vue";
export default defineComponent({
    setup() {
        console.log(inject('msg1').value) //子组件msg1
        console.log(inject('msg2').value) //子组件msg2
    },
});
</script>
```
**setup语法糖**
```js
//父组件
<script setup>
import Child from './Child'
import { ref,provide } from "vue";
const msg1 = ref('子组件msg1')
const msg2 = ref('子组件msg2')
provide("msg1",msg1)
provide("msg2",msg2)
</script>

//子组件
<script setup>
import { inject } from "vue";
console.log(inject('msg1').value) //子组件msg1
console.log(inject('msg2').value) //子组件msg2
</script>
```
provide/inject一般在深层组件嵌套中使用合适。一般在组件开发中用的居多。

### parent/children
$parent: 子组件获取父组件Vue实例，可以获取父组件的属性方法等

$children: 父组件获取子组件Vue实例，是一个数组，是直接儿子的集合，但并不保证子组件的顺序

**选项式API**
```js
import Child from './Child'
export default {
  components: {
    Child
  },
  created(){
    console.log(this.$children) //[Child实例]
    console.log(this.$parent)//父组件实例
  }
}
```
父组件获取到的$children并不是响应式的

### expose&ref
$refs可以直接获取元素属性，同时也可以直接获取子组件实例

**选项式API**
```js
//父组件
<template>
  <div>
    <Child ref="child" />
  </div>
</template>
<script>
import Child from './Child'
export default {
  components: {
    Child
  },
  mounted(){
    //获取子组件属性
    console.log(this.$refs.child.msg) //子组件元素

    //调用子组件方法
    this.$refs.child.childFun('父组件信息')
  }
}
</script>

//子组件 
<template>
  <div>
    <div></div>
  </div>
</template>
<script>
export default {
  data(){
    return {
      msg:'子组件元素'
    }
  },
  methods:{
    childFun(val){
      console.log(`子组件方法被调用,值${val}`)
    }
  }
}
</script>
```
**Vue3**
```js
//父组件
<template>
  <div>
    <Child ref="child" />
  </div>
</template>
<script>
import Child from './Child'
import { ref, defineComponent, onMounted } from "vue";
export default defineComponent({
  components: {
    Child
  },

  setup() {
    const child = ref() //注意命名需要和template中ref对应
    onMounted(() => {
      //获取子组件属性
      console.log(child.value.msg) //子组件元素

      //调用子组件方法
      child.value.childFun('父组件信息')
    })
    return {
      child //必须return出去 否则获取不到实例
    }
  },
});
</script>

//子组件
<template>
    <div>
    </div>
</template>
<script>
import { defineComponent, ref } from "vue";
export default defineComponent({
    setup() {
        const msg = ref('子组件元素')
        const childFun = (val) => {
            console.log(`子组件方法被调用,值${val}`)
        }
        return {
            msg,
            childFun
        }
    },
});
</script>
```
**setup语法糖**
```js
//父组件
<template>
  <div>
    <Child ref="child" />
  </div>
</template>
<script setup>
import Child from './Child'
import { ref, onMounted } from "vue";
const child = ref() //注意命名需要和template中ref对应
onMounted(() => {
  //获取子组件属性
  console.log(child.value.msg) //子组件元素

  //调用子组件方法
  child.value.childFun('父组件信息')
})
</script>

//子组件
<template>
    <div>
    </div>
</template>
<script setup>
import { ref,defineExpose } from "vue";
const msg = ref('子组件元素')
const childFun = (val) => {
    console.log(`子组件方法被调用,值${val}`)
}
//必须暴露出去父组件才会获取到
defineExpose({
    childFun,
    msg
})
</script>
```
通过ref获取子组件实例必须在页面挂载完成后才能获取。

在使用setup语法糖时候，子组件必须元素或方法暴露出去父组件才能获取到

### EventBus/mitt
兄弟组件通信可以通过一个事件中心EventBus实现，既新建一个Vue实例来进行事件的监听，触发和销毁。

在Vue3中没有了EventBus兄弟组件通信，但是现在有了一个替代的方案mitt.js，原理还是 EventBus

**Vue2**
```js
//组件1
<template>
  <div>
    <button @click="sendMsg">传值</button>
  </div>
</template>
<script>
import Bus from './bus.js'
export default {
  data(){
    return {
      msg:'子组件元素'
    }
  },
  methods:{
    sendMsg(){
      Bus.$emit('sendMsg','兄弟的值')
    }
  }
}
</script>

//组件2
<template>
  <div>
    组件2
  </div>
</template>
<script>
import Bus from './bus.js'
export default {
  created(){
   Bus.$on('sendMsg',(val)=>{
    console.log(val);//兄弟的值
   })
  }
}
</script>

//bus.js
import Vue from "vue"
export default new Vue()
```
**组合式API**

首先安装mitt `npm i mitt -S`
然后像Vue2中bus.js一样新建mitt.js文件
mitt.js
```
import mitt from 'mitt'
const Mitt = mitt()
export default Mitt
```
```js
//组件1
<template>
     <button @click="sendMsg">传值</button>
</template>
<script>
import { defineComponent } from "vue";
import Mitt from './mitt.js'
export default defineComponent({
    setup() {
        const sendMsg = () => {
            Mitt.emit('sendMsg','兄弟的值')
        }
        return {
           sendMsg
        }
    },
});
</script>

//组件2
<template>
  <div>
    组件2
  </div>
</template>
<script>
import { defineComponent, onUnmounted } from "vue";
import Mitt from './mitt.js'
export default defineComponent({
  setup() {
    const getMsg = (val) => {
      console.log(val);//兄弟的值
    }
    Mitt.on('sendMsg', getMsg)
    onUnmounted(() => {
      //组件销毁 移除监听
      Mitt.off('sendMsg', getMsg)
    })

  },
});
</script>
```
**setup语法糖**
```js
//组件1
<template>
    <button @click="sendMsg">传值</button>
</template>
<script setup>
import Mitt from './mitt.js'
const sendMsg = () => {
    Mitt.emit('sendMsg', '兄弟的值')
}
</script>

//组件2
<template>
  <div>
    组件2
  </div>
</template>
<script setup>
import { onUnmounted } from "vue";
import Mitt from './mitt.js'
const getMsg = (val) => {
  console.log(val);//兄弟的值
}
Mitt.on('sendMsg', getMsg)
onUnmounted(() => {
  //组件销毁 移除监听
  Mitt.off('sendMsg', getMsg)
})
</script>
```



## v-model和sync
v-model适用于双向绑定的指令，在vue2中，一个组件或者标签只能有一个v-model，并且默认属性和事件为value和input，也可以用于父子组件之间数据双向绑定。

#### v-model和sync在组件中的使用:
在Vue中的props是单向向下绑定的；每次父组件更新时，子组件中的所有props都会刷新为最新的值；但是如果在子组件中修改 props ，Vue会向你发出一个警告（无法在子组件修改父组件传递的值)；可能是为了防止子组件无意间修改了父组件的状态，来避免应用的数据流变得混乱难以理解。

但是可以在父组件使用子组件的标签上声明一个监听事件，子组件想要修改props的值时使用$emit触发事件并传入新的值，让父组件进行修改。

为了方便，vue就使用了v-model和sync语法糖。

### 选项式API
```js
//父组件
<template>
  <div>
   <!-- 
      完整写法
      <Child :msg="msg" @update:changePval="msg=$event" /> 
      -->
    <Child :changePval.sync="msg" />
    {{msg}}
  </div>
</template>
<script>
import Child from './Child'
export default {
  components: {
    Child
  },
  data(){
    return {
      msg:'父组件值'
    }
  }
  
}
</script>

//子组件
<template>
  <div>
    <button @click="changePval">改变父组件值</button>
  </div>
</template>
<script>
export default {
  data(){
    return {
      msg:'子组件元素'
    }
  },
  methods:{
    changePval(){
       //点击则会修改父组件msg的值
      this.$emit('update:changePval','改变后的值')
    }
  }
}
</script>
```
### setup语法糖
```js
//父组件
<template>
  <div>
    <!-- 
      完整写法
      <Child :msg="msg" @update:changePval="msg=$event" /> 
      -->
    <Child v-model:changePval="msg" />
    {{msg}}
  </div>
</template>
<script setup>
import Child from './Child'
import { ref } from 'vue'
const msg = ref('父组件值')
</script>

//子组件
<template>
    <button @click="changePval">改变父组件值</button>
</template>
<script setup>
import { defineEmits } from 'vue';
const emits = defineEmits(['changePval'])
const changePval = () => {
    //点击则会修改父组件msg的值
    emits('update:changePval','改变后的值')
}
</script>
```
**总结**
vue3中移除了sync的写法，取而代之的式v-model:event的形式

其v-model:changePval="msg"或者:changePval.sync="msg"的完整写法为
:msg="msg" @update:changePval="msg=$event"。

所以子组件需要发送update:changePval事件进行修改父组件的值。

## 路由
vue3和vue2路由常用功能只是写法上有些区别
### 选项式API
```js
<template>
  <div>
     <button @click="toPage">路由跳转</button>
  </div>
</template>
<script>
export default {
  beforeRouteEnter (to, from, next) {
    // 在渲染该组件的对应路由被 confirm 前调用
    next()
  },
  beforeRouteEnter (to, from, next) {
    // 在渲染该组件的对应路由被 confirm 前调用
    next()
  },
  beforeRouteLeave ((to, from, next)=>{//离开当前的组件，触发
    next()       
  }),
  beforeRouteLeave((to, from, next)=>{//离开当前的组件，触发
    next()      
  }),
  methods:{
    toPage(){
      //路由跳转
      this.$router.push(xxx)
    }
  },
  created(){
    //获取params
    this.$router.params
    //获取query
    this.$router.query
  }
}
</script>
```
**组合式API**
```js
<template>
  <div>
    <button @click="toPage">路由跳转</button>
  </div>
</template>
<script>
import { defineComponent } from 'vue'
import { useRoute, useRouter } from 'vue-router'
export default defineComponent({
  beforeRouteEnter (to, from, next) {
    // 在渲染该组件的对应路由被 confirm 前调用
    next()
  },
  beforeRouteLeave ((to, from, next)=>{//离开当前的组件，触发
    next()       
  }),
  beforeRouteLeave((to, from, next)=>{//离开当前的组件，触发
    next()      
  }),
  setup() {
    const router = useRouter()
    const route = useRoute()
    const toPage = () => {
      router.push(xxx)
    }

    //获取params 注意是route
    route.params
    //获取query
    route.query
    return {
      toPage
    }
  },
});
</script>
```


### 技术栈
#### Vue3
Vue3 官网及其介绍：https://v3.cn.vuejs.org/guide/introduction.html
#### TypeScript
TypeScript 官网文档：https://www.tslang.cn/
#### VueRouter
VueRouter 官网及其介绍： https://router.vuejs.org/zh/
#### Pinia
Pinia 官网及其介绍：https://pinia.web3doc.top/
#### Axios
Axios 官网及其介绍：http://www.axios-js.com/
#### Sass
Sass 官网及其介绍：https://www.sass.hk/
#### Element Plus
Element Plus 官网及其介绍：https://element-plus.gitee.io/zh-CN/guide/design.html