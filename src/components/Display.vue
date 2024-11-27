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
    <div class="display">
        <!-- Display de Histórico -->
        <div class="display__last-operation">
            <span class="display__last-operation__text">
                {{ historyDisplay }}
            </span>
        </div>
        <!-- Display Principal -->
        <input maxlength="21" type="text" class="display__text" :value="estado.valorCorrente" readonly>
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
        margin: 30px;
        border-left: solid 6px #E83D2A;
        border-radius: 5px;
        position: relative;

        .display__last-operation {
            position: absolute;
            top: 20px;
            right: 15px;
            color: rgb(150, 150, 150);
        }

        .display__text {
            width: 500px;
            height: 60px;
            background-color: transparent;
            /* border: solid 1px white; */
            border: none;
            position: absolute;
            bottom: 25px;
            right: 13px;
            font-size: 5em;
            color: white;
            text-align: right;
            font-weight: 500;
            caret-color: transparent;
        }

        .display__text:focus {
            outline: none;
        }
    }
</style>