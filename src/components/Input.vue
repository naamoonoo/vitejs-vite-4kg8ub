<script setup>
import { ref } from 'vue';

const model = ref('')

</script>

<template>
    <div class="container">
        <div c>
        <input v-model="model" class="input"/>
        <button>추가</button>
        </div>
    <div v-if="model.includes('x')" class="warning">사용할 수 없는 단어가 포함되어있어요.</div>
</div>

</template>

<style scoped>
.container {
    width:100%;
    padding: 0 8px;
    display: flex;    
    flex-direction: column
}

.input {
    width:100%;
}

.warning {
    color:red;
    text-align: center;
}
</style>
