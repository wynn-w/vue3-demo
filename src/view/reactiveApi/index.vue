<template>
  <div class="hello">
    <h1>Reactive API</h1>
    <section>
    <button @click="add">press</button>
      <div>
        <span>num: </span>{{state.num}}
        
        <span>demo: </span>{{demo}}
      </div>
    </section>
    <section>
      <button @click="change">demo value change</button>
      <section>
        <!-- 从 demo1 值的变化可以看出，逻辑层的值发生了变化，但视图层值未更改 -->
        <p>demo1: {{demo1}}</p>
        <!-- 由于两者引用是同一个对象，导致每次变更都 ++ 两次 -->
        <p>toRefsDemo1: {{toRefsDemo1}}</p>
        <p>toRefDemo1: {{toRefDemo1}}</p>
      </section>
    </section>

  </div>
</template>

<script>
import { reactive, toRefs, toRef } from 'vue' // volar 里面居然没有自动导入。。
export default {
  name: 'ReactiveApi',
  props: {
    msg: String
  },
  setup() {
    const state = reactive({
      num:0
    }); // 成为了响应式数据，接收复杂数据类型时为响应式数据
    let demo =  reactive(101) // 可以这样设值，但为非响应式 => 转跳 ref api 仅为基础数据类型数值开启响应式
    const add = () => {
      console.log(state.num);
      console.log(demo++);
      return state.num++
    }
    
    /* 增强 */
    
    // 对 reactive 对象直接解构而产生的数据为普通对象，不具备响应式能力
    let {demo1, demo2} = reactive({demo1: 1, demo2: 2}) // 等价于 let {demo1, demo2} = {demo1, demo2}

    // 对于上面的问题，官方提供的解决方案 ① toRefs(针对整个 reactive 对象)、②toRef(针对整个 reactive 对象的某个属性)
    // 如果直接使用 ref 方法则会导致两者无法联通，失去意义
    const toRefsValue = reactive({demo11: 1, demo12: 2});
    let {demo11:toRefsDemo1, demo12:toRefsDemo2} = toRefs(toRefsValue);
    let toRefDemo1 = toRef(toRefsValue, 'demo11');

    const change = () => {
      demo1++;
      toRefsDemo1.value++;
      toRefDemo1.value++;
      console.log('demo1',demo1);
      console.log('toRefsDemo1',toRefsDemo1);
      console.log('toRefDemo1',toRefDemo1);
    }


    return {
      toRefDemo1,
      toRefsDemo1,
      toRefsDemo2,
      demo1,
      demo2,
      state, // 从输出结果与页面展示结果来看，这样的的导出的 num 不是响应式的
      add,
      change,
      demo // 已经报警告了：value cannot be made reactive: 101
    }
  },
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
