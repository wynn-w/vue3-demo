<script>
import { h, ref } from 'vue';
export default {
    setup() {
        let num = ref(0);
        return () => {
            return h(
            'div',
            {
                class: 'm-render-container'
            },
            [
                h('p', {class:'show-value'}, num.value),
                h(
                    'button', 
                    {
                        onclick: ()=> num.value++ // 没有这样的简写 onclick(){...}
                    }, 
                    '+'
                ),
                h(
                    'button', 
                    {
                        onclick: ()=> num.value = 0 // 没有这样的简写 onclick(){...}
                    }, 
                    'reset'
                )
            ]
        )
        }
    },
    // render() {
    //     // return h('div', {}, 'sss') // 基础使用 第二个参数为 html 属性/方法，第三个参数为内容（innerHTML）
    //     return h(
    //         'div',
    //         {
    //             class: 'm-render-container'
    //         },
    //         [
    //             h('p', {class:'show-value'}, this.num),
    //             h(
    //                 'button', 
    //                 {
    //                     onclick: ()=> this.num++ // 没有这样的简写 onclick(){...}
    //                 }, 
    //                 '+'
    //             ),
    //             h(
    //                 'button', 
    //                 {
    //                     onclick: ()=> this.num = 0 // 没有这样的简写 onclick(){...}
    //                 }, 
    //                 'reset'
    //             )
    //         ]
    //     )
    // },
}
</script>
