<template>
  <div class="hello">
    <h1>Ref API</h1>
    <button @click="add">press</button>
    <div>
      <!-- 在 template 中自动结构 num.value 并将值赋值给 num -->
      <div>num: {{num}}</div>
      <!-- num.value 直接取不到值了，改了吗？ -->
      <div>num.value: {{num.value}}</div>
      <!-- 经测试发现以下三种情况都可 ref 解包 -->
      <!-- 与传闻中的 ref 只能浅层解包不相符 -->
      <div>baseNum.num: {{baseNum.num}}</div>
      <div>baseNum.num.value: {{baseNum.num.value}}</div>
      <div>baseNum: {{baseNum}}</div>
      
      <div>reactNum.num: {{reactNum.num}}</div>
      <div>reactNum.num.value: {{reactNum.num.value}}</div>
      <div>reactNum: {{reactNum}}</div>
    </div>
    <section>
      <button @click="updateShallowValue">update demo</button>
      <p>shallw ref: demo => {{shallowValue.demo}}</p>
      <button @click="triggerRefForShallowValue">update str</button>
      <p>shallw ref: str => {{shallowValue.str}}</p>
    </section>
  </div>
</template>

<script>
import { reactive, ref, shallowRef, triggerRef } from 'vue' 
export default {
  name: 'RefApi',
  props: {
    msg: String
  },
  setup() {
    const num = ref(0)
    const baseNum = {
      num
    }
    const reactNum = reactive({
      num
    })
    // 而在 Javascript 中需要手动调用 .value 属性进行值操作
    const add = () => {
      console.log(num.value);
      return num.value++
    }
    // =========================================== 补充：
    
    /**
     * 关于使用 ref 操作对象问题（官网默认用作 基础数据类型 操作） 
     * 用了一下的感受，我为什么需要用 ref 操作对象，这不还提供 shallowReactive 吗
    */
    
    /* 浅层响应式数据 shallowRef */  
    // 据说引入的原因是在不期望所有数据均响应式的场景下使用（最外层）
    const shallowValue = shallowRef({demo: 2, str: 'a str'}); // 从代码提示可以看到官方还提供 shallowReactive/Readonly
    const updateShallowValue = () =>{
      ++shallowValue.value.demo;
      console.log(shallowValue.value.demo); // 从打印数据与视图数据对比发现，视图数据未同步 
                                            // => 未实现数据响应式 
                                            // => 这里的浅层响应式是指什么？ 
                                            // => 最外层数据（对象）被覆盖时为响应式，内部数据变更不监听
    }
    const triggerRefForShallowValue = () => {
      // 针对上面的情况，官方提供了 triggerRef
      shallowValue.value.str = 'str is update';
      triggerRef(shallowValue); // 通过主动调用的方式来达到数据刷新的效果，像极了 vue2 中的 $forceUpdate()
                                // 从打包代码来看，生产环境将 newVal 赋值为 void 0 是什么个意思？
      console.log(shallowValue.value.str); // 视图与逻辑层数据都发生了变更
    }
    return {
      num,
      baseNum,
      reactNum,
      add,
      updateShallowValue,
      triggerRefForShallowValue,
      shallowValue
    }
  }
  // setup(props, content) {
    // console.log(props) // Proxy
    // console.log(content) // attrs, emit, expose, slots
  // }
  
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
