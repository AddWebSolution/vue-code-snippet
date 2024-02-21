<template>
    <button v-longpress='longPressDetected'>Longpress me!!</button>
</template>

<script>
const PRESS_TIMEOUT = 1000

Vue.directive('longpress', {
    bind: function (el, { value }, vNode) {
        if (typeof value !== 'function') {
            console.warn(`Function Expected, got ${value}`)
            return
        }

        let pressTimer = null

        const start = e => {
            if (e.type === 'click' && e.button !== 0) {
                return;
            }

            if (pressTimer === null) {
                pressTimer = setTimeout(() => value(e), PRESS_TIMEOUT)
            }
        }

        const cancel = () => {
                if (pressTimer !== null) {
                    clearTimeout(pressTimer)
                    pressTimer = null
                }
            }

        ;['mousedown', 'touchstart'].forEach(e => el.addEventListener(e, start))
        ;['click', 'mouseout', 'touchend', 'touchcancel'].forEach(e => el.addEventListener(e, cancel))
    }
})


export default {
    methods: {
        longPressDetected () {
            // Write your logic here
        }
    }
}
</script>
