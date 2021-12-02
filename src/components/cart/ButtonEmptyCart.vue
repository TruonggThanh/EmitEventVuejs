<template>
    <div class="button-empty-cart">
        <button class="button" @click="buttonClicked()">
            <slot></slot>
        </button>
    </div>
</template>

<script>
export default {
    name: 'ButtonEmptyCart',
    components: {},
    data() {
        return {}
    },
    methods: {
        buttonClicked() {
            this.$emit('emit-empty-cart')
        }
    }
}
</script>

<style scoped>

</style>