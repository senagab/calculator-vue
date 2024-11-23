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