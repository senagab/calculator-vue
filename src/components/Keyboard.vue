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
<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Inter:ital,opsz,wght@0,14..32,100..900;1,14..32,100..900&display=swap');


* {
    padding: 0;
    margin: 0;
    box-sizing: border-box;
    font-family: 'Inter', sans-serif;
}

header {
    color: #bdbdbd;
}

.container {
    display: flex;
    flex-direction: column;
    width: 40%;
    min-width: 35em;
    margin: 0 auto;
    height: 100%;
    background-color: black;
    border-radius: 5px;
    filter: drop-shadow(3px 3px 0.75rem rgba(255, 255, 255, 0.1));
}

.keyboard {
    margin: -15px 30px 30px;
    display: flex;
    justify-content: space-around;

    .keyboard__left {
        display: grid;
        grid-template-columns: 1fr 1fr 1fr;
        gap: 1rem;

        .keys {
            width: 10vh;
            height: 10vh;
            display: flex;
            justify-content: center;
            align-items: center;
            background-color: black;
            font-size: 30px;
            color: rgb(128, 128, 128);
        }

        .keys:hover {
            background-color: #1a1a1a;
            color: rgb(206, 206, 206);
            cursor: pointer;
        }

        .keys:active {
            background-color: #2b2b2b;
            color: rgb(255, 255, 255);
            font-weight: bold;
            font-size: 25px;
        }

        .keys.active {
            background-color: #2b2b2b;
            color: rgb(255, 255, 255);
            font-weight: bold;
            font-size: 25px;
        }
    }

    .keyboard__center {
        display: grid;
        grid-template-columns: 1fr;
        gap: 1rem;

        .keys {
            width: 10vh;
            height: 10vh;
            display: flex;
            justify-content: center;
            align-items: center;
            background-color: black;
            font-size: 30px;
            color: rgb(138, 138, 138);
        }

        .keys:hover {
            background-color: #1a1a1a;
            color: rgb(206, 206, 206);
            cursor: pointer;
        }

        .keys:active {
            background-color: #2b2b2b;
            color: rgb(255, 255, 255);
            font-weight: bold;
            font-size: 20px;
        }

        .keys.active {
            background-color: #2b2b2b;
            color: rgb(255, 255, 255);
            font-weight: bold;
            font-size: 25px;
        }
    }

    .keyboard__right {
        display: grid;
        grid-template-columns: 50px;
        grid-template-rows: 1fr 1fr 2fr;
        gap: 1rem;
        margin: 0 15px;

        .keys {
            width: 10vh;
            height: 10vh;
            display: flex;
            justify-content: center;
            align-items: center;
            background-color: black;
            padding: 30px;
            font-size: 30px;
            color: rgb(138, 138, 138);
        }

        .btn-backspace {
            background-image: url('../assets/images/backspace.svg');
            background-position: center;
            background-repeat: no-repeat;
            background-size: contain;
            padding: 0 !important;
        }

        .btn-equals {
            background-image: url('../assets/images/equals.png');
            background-position: center;
            background-repeat: no-repeat;
            background-size: cover;
            padding: 0 !important;
        }

        .keys:hover {
            background-color: #232323;
            cursor: pointer;
        }

        .keys:active {
            background-color: #2b2b2b;
            color: rgb(255, 255, 255);
            font-weight: bold;
            font-size: 25px;
        }

        .keys.active {
            background-color: #2b2b2b;
            color: rgb(255, 255, 255);
            font-weight: bold;
            font-size: 25px;
        }
    }
}
</style>