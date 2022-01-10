<script>
import mSlot from './mSlot.vue';
import { h, ref } from 'vue';
export default {
    setup() {
        let num = ref(1);
        return () => {
            return h(
                'div', 
                {
                    class: 'lala'
                }, 
                [
                    h('p', null, 'dadada...'),
                    h(mSlot, {}, `num: ${num.value}`), // 从视图展示结果来看，任意值进去都走 default 插槽
                    h(mSlot, {}, 
                    {
                        default: () => h('span', null, `default slot change`),
                        setName: () => h('span', null, `setName slot change`), // 具名插槽
                        sendProps: (props) => h('span', null, `sendProps slot: ${props.msg}`), // 作用域插槽
                    }
                    ), 

                    h('p', null, 'dadada...')
                ]
            );
        }
    }

    // ==================================================== setup render --base
    // setup() {
    //     let num = ref(0);
    //     return () => {
    //         return h(
    //         'div',
    //         {
    //             class: 'm-render-container'
    //         },
    //         [
    //             h('p', {class:'show-value'}, num.value),
    //             h(
    //                 'button', 
    //                 {
    //                     onclick: ()=> num.value++ // 没有这样的简写 onclick(){...}
    //                 }, 
    //                 '+' 
    //             ),
    //             h(
    //                 'button', 
    //                 {
    //                     onclick: ()=> num.value = 0 // 没有这样的简写 onclick(){...}
    //                 }, 
    //                 'reset'
    //             )
    //         ]
    //     )
    //     }
    // },
    // =================================================== render function
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
