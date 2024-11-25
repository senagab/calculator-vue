<script setup>
const props = defineProps({
    valor: {
        type: String,
        required: true,
    },
    historico: {
        type: String,
        required: true,
    },
});
</script>

<template>
    <!-- Display de Histórico -->
    <div class="display__last-operation">
        <span class="display__last-operation__text">
            {{ historico }}
        </span>
    </div>
    <!-- Display Principal -->
    <input maxlength="21" type="text" class="display__text" :value="valor" readonly>
</template>