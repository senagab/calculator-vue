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
    raizQuadrada: Function
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
            <!-- <div @click="props.raizQuadrada" class="keys" style="color: gray;">√</div> -->
            <!-- <div @click="props.raizQuadrada" class="keys" data-key="raizQuadrada" style="color: gray;">√</div> -->
            <div @click="props.raizQuadrada" class="keys" data-key="raizQuadrada" style="color: gray;">√</div>

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
            <div @click="props.limpar" class="keys keys-limpar" data-key="limpar">C</div>
            <div @click="props.resultado" class="keys btn btn-equals" data-key="resultado">=</div>
        </div>
    </div>
</template>
<style scoped>
.keyboard {
    margin: 30px 30px;
    display: flex;
    justify-content: space-evenly;
    max-height: 22em;

    .keyboard__left {
        display: grid;
        grid-template-columns: 1fr 1fr 1fr;
        column-gap: 1rem;
        align-items: center;
        justify-content: center;

        .keys {
            width: 12vh;
            height: 12vh;
            display: flex;
            justify-content: center;
            align-items: center;
            background-color: black;
            font-size: 45px;
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
        align-items: center;
        justify-content: center;
        margin: 0 30px;

        .keys {
            width: 12vh;
            height: 12vh;
            display: flex;
            justify-content: center;
            align-items: center;
            background-color: black;
            font-size: 45px;
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
        grid-template-rows: 1fr 1fr 3fr;
        gap: 1rem;
        margin: 0 15px;
        justify-content: center;
        align-items: center;

        .keys {
            /* width: 12vh; */
            height: 12vh;
            display: flex;
            justify-content: center;
            align-items: center;
            background-color: black;
            padding: 0;
            font-size: 30px;
            color: rgb(138, 138, 138);
        }

        .btn-backspace {
            background-image: url('../assets/images/backspace.svg');
            background-position: center;
            background-repeat: no-repeat;
            background-size: contain;
            padding: 0 !important;

            &:hover {
                filter: brightness(120%);
                background-color: black !important;
            }
        }

        .keys-limpar {
            font-size: 45px;
        }

        .btn-equals {
            color: white;
            background: linear-gradient(to top right, #FF2107, #5E0A00);
            min-width: 100%;
            width: 100%;
            min-height: 2.5em;
            height: 100%;
            padding: 0 !important;
            font-size: 45px;

            &:hover {
                background: linear-gradient(to top right, #ff4934, #9b1a0b);
            }
        }

        .keys:hover {
            background-color: #232323;
            cursor: pointer;
        }

        .keys.active {
            background-color: #2b2b2b;
            color: rgb(255, 255, 255);
            font-weight: bold;
            font-size: 25px;
        }

        .keys.active-limpar {
            filter: brightness(150%);
            background-color: black !important;
        }

        .keys.active-resultado {
            background: linear-gradient(to top right, #ff7f70, #ff2e17);
            color: black;
        }
    }

}

@media (max-width: 640px) {

    .keyboard {
        margin: 30px 30px;
        display: flex;
        justify-content: center;
        max-height: 22em;

        .keyboard__left, 
        .keyboard__center {

            .keys {
                width: 5vh;
                height: 5vh;
                font-size: 25px;
                /* color: red; */
            }
        }

        .keyboard__right {
            margin: 0;

            .keys-limpar {
                height: 4vh;
                font-size: 25px;
                /* background-color: #ddd;
                height: 8vh; */
            }

            .btn-equals {
                height: 80%;
                margin-top: -10px;
                font-size: 25px;
            }
        }
    }
}
</style>