<template>
    <h3>歷史紀錄</h3>
    <ul id="list" class="list">
        <li v-for="item in transactions" :class="item.amount > 0 ? 'plus' : 'minus'" :key="item.id">
            {{ item.text }} <span>{{ item.amount.toLocaleString() }}</span> <button class="delete-btn"
                @click="$emit('delete', item.id)">X</button>
        </li>
    </ul>
</template>


<script setup>
import { defineEmits } from 'vue'

const props = defineProps({
    transactions: {
        type: Array,
        required: true,
    }
})

const emit = defineEmits(['delete'])

</script>


<style scoped></style>