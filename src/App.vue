<template>
    <div id="app">
        <h1>Problema de Monty Hall</h1>
        <div v-if="!started" class="form">
            <div>
                <label for="portsAmount">Quantas portas?</label>
                <input
                    type="number"
                    id="portsAmount"
                    min="1"
                    v-model.number="portsAmount">
            </div>
            <div>
                <label for="selectedPort">Qual a porta premiada?</label>
                <input
                    type="number"
                    id="selectedPort"
                    min="1"
                    :max="portsAmount"
                    v-model.number="selectedPort">
            </div>

            <button class="btn" @click="started = true">Iniciar</button>
        </div>

        <div v-else class="result">
            <button class="btn" @click="started = false">Reiniciar</button>

            <div class="doors">
              <div v-for="i in portsAmount" :key="i">
                <Door :hasGift="i === selectedPort" :number="i" />
              </div>
            </div>
        </div>
    </div>
</template>

<script>
import Door from './components/Door'
export default {
    name: 'App',
    components: { Door },
    data: function() {
        return {
            started: false,
            portsAmount: 3,
            selectedPort: 1
        }
    }
}
</script>

<style>
:root {
    --border-radius: 8px;
}

* {
    box-sizing: border-box;
    font-family: 'Montserrat', sans-serif;
}

body {
    color: #FFF;
    background: linear-gradient(to right, rgb(21, 153, 87), rgb(21, 87, 153));
}

#app {
    display: flex;
    flex-direction: column;
    align-items: center;
    font-size: 1rem;
}

#app h1 {
    border: 1px solid #0004;
    background-color: #0004;
    border-radius: var(--border-radius);
    font-size: 1.2em;
    line-height: 1;
    margin: 30px 0 60px;
    padding: 20px 30px;
    text-align: center;
}

.form {
    display: flex;
    flex-direction: column;
    align-items: stretch;
    margin-bottom: 40px;
    text-align: center;
}

.form div {
    width: 100%;
    margin-bottom: 30px;
}

.form label {
    display: block;
    margin-bottom: 10px;
}

.form input {
    box-sizing: border-box;
    background: #fff2;
    border-radius: var(--border-radius);
    border: solid 2px #0004;
    color: #fff;
    display: block;
    font-size: 1.2em;
    padding: 10px 35px;
    text-align: center;
    width: 100%;
}

.form input:focus {
    outline: none;
    border-color: #0007;
}

.form input[type=number]::-webkit-inner-spin-button {
    -webkit-appearance: none;
}

.btn {
    cursor: pointer;
    color: #fff;
    font-size: 1em;
    text-transform: uppercase;
    padding: 15px 35px;
    background: #0004;
    border: 0;
    border-radius: var(--border-radius);
    transition: .3s ease;
}

.btn:hover {
    transform: scale(1.1);
    background: #0006;
}

.btn:focus {
    outline: none;
}

.result {
    display: flex;
    flex-direction: column;
    align-items: center;
    margin-bottom: 60px;
}

.doors {
    margin-top: 40px;
    align-self: stretch;
    display: flex;
    justify-content: center;
    flex-wrap: wrap;
}

@media screen and (min-width: 768px) {
    #app {
        font-size: 1.5rem;
    }
}
</style>
