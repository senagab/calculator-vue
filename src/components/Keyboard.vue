<script setup>

const props = defineProps({
    juntarNumeros: Function,
    ponto: Function,
    somar: Function,
    diminuir: Function,
    multiplicar: Function,
    dividir: Function,
    backspace: Function,
    limpar: Function,
    resultado: Function,
});

</script>

<template>
    <div class="keyboard">
        <div class="keyboard__left">
            <div @click="props.juntarNumeros(7)" class="keys" data-key="7">7</div>
            <div @click="props.juntarNumeros(8)" class="keys" data-key="8">8</div>
            <div @click="props.juntarNumeros(9)" class="keys" data-key="9">9</div>
            <div @click="props.juntarNumeros(4)" class="keys" data-key="4">4</div>
            <div @click="props.juntarNumeros(5)" class="keys" data-key="5">5</div>
            <div @click="props.juntarNumeros(6)" class="keys" data-key="6">6</div>
            <div @click="props.juntarNumeros(1)" class="keys" data-key="1">1</div>
            <div @click="props.juntarNumeros(2)" class="keys" data-key="2">2</div>
            <div @click="props.juntarNumeros(3)" class="keys" data-key="3">3</div>
            <div @click="props.juntarNumeros(0)" class="keys" data-key="0">0</div>
            <div @click="props.ponto" class="keys" style="color: gray;">,</div>
            <div @click="props.raizQuadrada" class="keys" style="color: gray;">√</div>
        </div>
        <div class="keyboard__center">
            <div @click="props.dividir" class="keys keys--div" data-key="dividir">/</div>
            <div @click="props.multiplicar" class="keys keys--mult" data-key="multiplicar">x</div>
            <div @click="props.diminuir" class="keys keys--sub" data-key="diminuir">-</div>
            <div @click="props.somar" class="keys keys--sum" data-key="somar">+</div>
        </div>
        <div class="keyboard__right">
            <div @click="props.backspace" class="keys btn btn-backspace" data-key="backspace" style="border: none;">
            </div>
            <div @click="props.limpar" class="keys" data-key="limpar">C</div>
            <div @click="props.resultado" class="keys btn btn-equals" data-key="resultado" style="height: 21vh;"></div>
        </div>
    </div>
</template>
