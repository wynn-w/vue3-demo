<template>
  <div class="hello">
    <h1>Ref API</h1>
    <button @click="add">press</button>
    <div>
      <!-- 在 template 中自动结构 num.value 并将值赋值给 num -->
      <span>num: </span>{{num}}
      <br>
      <!-- num.value 直接取不到值了，改了吗？ -->
      <span>num.value: </span>{{num.value}}
    </div>
  </div>
</template>

<script>
import { ref } from 'vue' // volar 里面居然没有自动导入。。
export default {
  name: 'RefApi',
  props: {
    msg: String
  },
  setup() {
    const num = ref(0)
    // 而在 Javascript 中需要手动调用 .value 属性进行值操作
    const add = () => {
      console.log(num.value);
      return num.value++
    }
    return {
      num,
      add,
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
