<script setup>
// import { defineProps } from 'vue';

// Recebendo `estado` e `historyDisplay` como props
const props = defineProps({
    estado: Object,
    historyDisplay: String,
});
</script>

<template>
    <div class="display">
        <!-- Display de Histórico -->
        <div class="display__last-operation">
            <span class="display__last-operation__text">
                {{ props.historyDisplay }}
            </span>
        </div>
        <!-- Display Principal -->
        <input maxlength="21" type="text" class="display__text" :value="props.estado.valorCorrente" readonly>
    </div>
</template>

<style scoped>
.display {
    display: flex;
    align-items: center;
    justify-content: center;
    height: 20vh;
    width: auto;
    background-color: #232323;
    margin: 30px 30px 0;
    border-left: solid 6px #E83D2A;
    border-radius: 5px;
    position: relative;

    .display__last-operation {
        position: absolute;
        top: 40px;
        right: 15px;
        color: rgb(150, 150, 150);
        font-size: 36px;
    }

    .display__text {
        width: 500px;
        height: 100px;
        background-color: transparent;
        /* border: solid 1px white; */
        border: none;
        position: absolute;
        bottom: 45px;
        right: 13px;
        font-size: 8.5em;
        color: white;
        text-align: right;
        font-weight: 500;
        caret-color: transparent;
    }

    .display__text:focus {
        outline: none;
    }
    
    @media (max-width: 640px) {

        height: 20vh !important;
        
        .display__last-operation {
            font-size: 18px;
            top: 15px;
            right: 15px;
        }

        .display__text {
            height: 60px;
            width: 4em;
            font-size: 4em;
            bottom: 15px;
            right: 13px;
        }
    }
}

</style>