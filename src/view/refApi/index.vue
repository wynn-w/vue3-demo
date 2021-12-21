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
  </div>
</template>

<script>
import { reactive, ref } from 'vue' // volar 里面居然没有自动导入。。
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
    return {
      num,
      baseNum,
      reactNum,
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
