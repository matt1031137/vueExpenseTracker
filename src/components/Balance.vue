<template>
    <h4>合計金額</h4>
    <h1 id="balance">${{ total.toLocaleString() }}</h1>
</template>


<script setup>

const props = defineProps({
    total: {
        type: Number,
        require: true,
    }
})



</script>



<style scoped></style>