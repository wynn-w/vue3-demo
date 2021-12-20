<template>
  <div class="hello">
    <h1>Reactive API</h1>
    <button @click="add">press</button>
    <div>
      <span>num: </span>{{state.num}}
      <span>demo: </span>{{demo}}
    </div>
  </div>
</template>

<script>
import { reactive } from 'vue' // volar 里面居然没有自动导入。。
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
    return {
      state, // 从输出结果与页面展示结果来看，这样的的导出的 num 不是响应式的
      add,
      demo
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
