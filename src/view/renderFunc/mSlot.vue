<script>
import { h } from 'vue';
export default {
    setup(props, {slots}) {
        return () => {
            return h(
                'div', 
                null, 
                [
                    h('p', null, 'there has a slot 👇'),
                    h(
                        'div', 
                        null,
                        slots.default ? slots.default() : h('span', null, 'default slot placehold'), 
                    ),
                    // null,
                    // `${slots}`
                    h(
                        'div', 
                        null,
                        slots.setName ? slots.setName() : h('span', null, 'setName slot placehold')
                    ),
                    h(
                        'div', 
                        null,
                        slots.sendProps ? slots.sendProps({msg: 'slot msg'}) : h('span', null, '')
                    )
                ]
            )
        }
    }
}
</script>