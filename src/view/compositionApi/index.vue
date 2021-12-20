<template>
  <div class="hello">
    <h1>Composition API</h1>
    <button @click="add">press</button>
    <div>
      <span>num: </span>{{num}}
    </div>
  </div>
</template>

<script>
export default {
  name: 'Compostion-Api',
  props: {
    msg: String
  },
  setup() {
    let num = 0;
    const add = () => {
      console.log(num);
      return num++
    }
    return {
      num, // 从输出结果与页面展示结果来看，这样的的导出的 num 不是响应式的
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
