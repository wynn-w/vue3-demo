<script>
import { reactive, ref } from 'vue';
export default {
    setup() {
        const aa = ref('xiaoming');
        const arr = reactive([1,2,4]);
        return {
            aa,
            arr
        }
    },
    render(){
        return (
            <div>
                <h1 style="margin: 0 auto">JSX code</h1>
                <p>aa: {this.aa}</p>
                <p>use Javascript generate HTMLElement</p>
                {
                    this.arr.map(item => (<p>{item}</p>))
                }
            </div>

        )
    }
}
</script>