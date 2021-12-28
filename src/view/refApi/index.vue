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
import { reactive, ref, shallowRef, triggerRef, customRef } from 'vue' 
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
    
    // =========================================== 补充：

    /**
     * customRef使用
     * */ 
    
    // 对于其使用场景
    // 1. 官网的输入框防抖：https://v3.cn.vuejs.org/api/refs-api.html#customref
    // 2. 加强型 computed(vue3 computed 不提供 set？)：https://cdmana.com/2021/12/202112181945339560.html
    // 3. 复杂同步方法的双向绑定：https://www.cnblogs.com/fsg6/p/14485972.html
    //    => 文章中指出 setup 函数是仅支持同步方法的（为什么不支持异步，值得浅度探究。。）
    const useCustomRef = (value) => {
      // track 通知监听数据 => value 值指向的数据
      // trigger 通知视图层同步更新的数据
      // customRef 要求回调函数必须要返回一个对象，且对象必须实现 get/set 方法
      return customRef((track, trigger)=>{
        // 就单从 get/set 看，与普通 es6 的方法其实没啥区别。核心还是在 track/trigger 方法上
        return {
          get(){
            track();
            return value;
          },
          set(newVal){
            value = newVal;
            trigger();
          }
        }
      })
    }
    return {
      num,
      baseNum,
      reactNum,
      add,
      updateShallowValue,
      triggerRefForShallowValue,
      shallowValue,
      useCustomRef
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
