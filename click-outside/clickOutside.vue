<template>
    <div v-clickoutside="outsideClicked">Click Outside of me....</div>
</template>

<script>
Vue.directive('clickoutside', {
    bind (el, { value }) {
        if (typeof value !== 'function') {
            console.warn(`Function Expected, got ${value}`)
            return
        }

        document.addEventListener('click', e => el.contains(e.target) || value())
    }
})

export default {
    methods: {
        outsideClicked () {
            // Write your logic here
        }
    }
}
</script>