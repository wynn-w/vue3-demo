<template>
  <div class="hello">
    <h1>Computed</h1>
    <section>
        <button @click="changeConcatDemoString2">change concatDemoString2</button>
        <p>concatDemoString: {{concatDemoString}}</p>
        <p>concatDemoString2: {{concatDemoString2}}</p>
    </section>
    <section>
        <button @click="addNum">add num</button>
        <p>num1: {{num1}}</p>
    </section>
  </div>
</template>

<script>
import { ref, computed, watchEffect } from 'vue' 
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
    // => 总结起来就是跟 vue2 没啥区别

    // watchEffect
    let num1 = ref(-1 );
    watchEffect(() => {
        console.log('watch effect:',`num1 => ${num1.value}`); // 甚至没有发生改变，就自动执行了 => 考虑替换 filter ？
    })

    const finishWatchEffect = watchEffect((arg) => {
        console.log(arg); // 里面是一个函数，函数中还包了一个回调: cleanup = effect.onStop 
                          // => 据描述是清除额外的副作用 => 取消某些操作？
        console.log('finishWatchEffect:',`num1 => ${num1.value}`); // 甚至没有发生改变，就自动执行了 => 考虑替换 filter ？
    });
    const addNum = () =>{
        ++num1.value
        if(num1.value > 1){
            finishWatchEffect(); // 监听停止（获取 watchEffect 的回调并执行），但函数每次触发时候，逻辑层与视图层数据任然同步变动
        }
    }
    
    return {
        concatDemoString,
        concatDemoString2,
        changeConcatDemoString2,
        addNum,
        num1
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
