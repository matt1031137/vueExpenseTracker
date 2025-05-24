<template>
    <div class="inc-exp-container">
        <div>
            <h4>收入</h4>
            <p id="money-plus" class="money plus">+${{income.toLocaleString()}}元</p>
        </div>

        <div>
            <h4>支出</h4>
            <p id="money-minus" class="money minus">-${{-expense.toLocaleString()}}元</p>
        </div>



    </div>

</template>



<script setup>

const props = defineProps({
    income: {
        type: Number,
        required: true
    },
    expense: {
        type: Number,
        required: true
    }
})


</script>




<style scoped></style>