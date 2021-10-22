<template>
    <button :style="{ backgroundColor: buttonColor }" @click="trackColor" class="add-btn"></button> 
</template>

<script>
export default {
    data() {
        return {
            selectedColor: '',
        }
    },
    props: {
        buttonColor: String,
    },
    methods: {
        trackColor() {
            this.selectedColor = this.buttonColor;
            this.$emit('buttonClick', this.selectedColor);
        }
    }
};
</script>

<style>
    .add-btn {
        width: 5rem;
        height: 5rem;
        border-radius: 50%;
        border: .1rem solid;
        cursor: pointer;
    }
</style>