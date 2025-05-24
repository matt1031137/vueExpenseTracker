<template>
    <h3>追加記帳條</h3>
    <form id="form" @submit.prevent="onSubmit">
        <div class="form-control">
            <label for="text">內容</label>
            <input type="text" id="text" v-model="text" placeholder="輸入內容...">
        </div>

        <div class="form-control">
            <label for="amount">金額</label>
            <input type="number" id="amount" v-model="amount" placeholder="+為收入 -為支出">
        </div>

        <button class="btn">追加</button>

    </form>
</template>

<script setup>
import { ref } from 'vue'
import { useToast } from 'vue-toastification'

const text = ref('')
const amount = ref('')

const emit = defineEmits(['addTransactions'])

const toast = useToast()

const onSubmit = () => {
    if (!text.value || !amount.value) {
        toast.error('內容跟金額不能空白！')
        return
    }

    const transactionData = {
        text:text.value,
        amount:parseInt(amount.value)
    }

    emit('addTransactions',transactionData)
    text.value = ''
    amount.value = ''

    toast.success('追加成功!')

}




</script>


<style scoped></style>