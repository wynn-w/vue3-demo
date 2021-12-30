<template>
  <div class="hello">
    <h1>Computed</h1>
    <section>
        <button @click="changeConcatDemoString2">change concatDemoString2</button>
        <p>concatDemoString: {{concatDemoString}}</p>
        <p>concatDemoString2: {{concatDemoString2}}</p>
    </section>
  </div>
</template>

<script>
import { ref, computed } from 'vue' 
export default {
  name: 'ComputedAndWatch',
  setup() {
    let demo1 = ref('demo1');
    let demo2 = ref('demo2');
    let demo3 = ref('demo3');
    let demo4 = ref('demo4');
    // computed 返回了一个 ComputedRef => 还是 ref 
    let concatDemoString = computed(() => `${demo1.value} ${demo2.value}`)
    let concatDemoString2 = computed({
        get: () => {
            return `${demo3.value} ${demo4.value}`
        },
        set: (newVlaue) => {
            const arr = newVlaue.split(' ')
            if(arr.length > 2){
                const d1 = arr[0];
                const d2 = arr[1];
                demo3.value = d1;
                demo4.value = d2;
            }
            else{
                // do something
            }
        }
    })
    const changeConcatDemoString2 = () => {
        demo3.value = 'change'; 
        demo4.value = 'value'; 
    }
    return {
        concatDemoString,
        concatDemoString2,
        changeConcatDemoString2
    }
  }
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
