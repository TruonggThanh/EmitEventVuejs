<template>
    <div class="button-add-cart">
        <button class="button" @click="buttonClicked()">
            <slot></slot>
        </button>
    </div>
</template>

<script>
export default {
    name: 'ButtonAddCart',
    props: ['item'],
    components: {},
    methods: {
        buttonClicked() {
            this.$emit('button-clicked');
        }
    }
}
</script>

<style scoped>

</style>