<template>
  <div class="hello">
    <h1>Ref API</h1>
    <button @click="add">press</button>
    <div>
      <!-- 在 template 中自动结构 num.value 并将值赋值给 num -->
      <div>num: {{num}}</div>
      <div>readonlynum: {{readonlyNum}}</div>

    </div>
  </div>
</template>

<script>
import { readonly } from 'vue' // volar 里面居然没有自动导入。。
export default {
  name: 'ReadonlyApi',
  props: {
    msg: String
  },
  setup() {
    const num = {
      num: 10
    }
    const readonlyNum = readonly(num)
    const add = () => {
      console.log(++readonlyNum.num);
      console.log(readonlyNum.num);
      return ;
    }
    // 通过 dist 目录下的代码可以知道这个也是 proxy 代理通过拦截实现的。不是通过 object.freeze 冻结的
    return {
      num,
      readonlyNum,
      add
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
