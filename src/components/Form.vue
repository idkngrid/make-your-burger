<template>
    <div>
        <Message :msg="msg" v-show="msg" />
    </div>
        <form class="form" @submit="createBurger">
            <div class="input-container">
                <label for="name" class="label">Nome</label>
                <input type="text" id="name" class="input" v-model="name" placeholder="Digite o seu nome">
            </div>
            <div class="input-container">
                <label for="bread" class="label">Escolha o pão: </label>
                <select name="bread" id="bread" class="input" v-model="bread">
                    <option value="" disabled>Selecione o seu pão</option>
                    <option v-for="bread in breads" :key="bread.id" :value="bread.tipo">{{ bread.tipo }}</option>
                </select>
            </div>
            <div class="input-container">
                <label for="meat" class="label">Escolha a carne do seu Burger: </label>
                <select name="meat" id="meat" class="input" v-model="meat">
                    <option value="" disabled>Selecione sua carne</option>
                    <option v-for="meat in meats" :key="meat.id" :value="meat.tipo">{{ meat.tipo }}</option>
                </select>
            </div>
            <div class="additional-container">
                <label for="additional" class="label additional-label">Selecione os adicionais: </label>
                <div class="checkbox-container" v-for="additional in additionalData" :key="additional.id">
                    <input type="checkbox" name="additionals" id="additionals" class="input checkbox" v-model="additionals" :value="additional.tipo">
                    <span>{{ additional.tipo }}</span>
                </div>
            </div>
            <div>
                <input type="submit" class="submit-btn" value="Criar meu Burger">
            </div>
        </form>
</template>
<script>
import Message from './Message.vue'

export default {
    name: 'Form',
    data() {
        return {
            breads: null,
            meats: null,
            additionalData: null,
            name: null,
            bread: null,
            meat: null,
            additionals: [],
            status: "Solicitado",
            msg: null
        }
    },
    methods: {
        async getIngredients() {
            const req = await fetch("http://localhost:3000/ingredientes");
            const data = await req.json();

            this.breads = data.paes;
            this.meats = data.carnes;
            this.additionalData = data.opcionais;
        },
        async createBurger(e) {
            e.preventDefault();

            const data = {
                name: this.name,
                bread: this.bread,
                meat: this.meat,
                additionals: Array.from(this.additionals),
                status: "Solicitado"
            }
            
            const dataJson = JSON.stringify(data);
            
            const req = await fetch("http://localhost:3000/burgers", {
                method: "POST",
                headers: { "Content-Type": "application/json" },
                body: dataJson
            })

            const res = await req.json();
            
            // msg de sistema
            this.msg = `Pedido nº ${res.id} realizado com sucesso!`

            // limpar msg
            setTimeout(() => this.msg = "", 3000);

            // limpar os campos
            this.name = "";
            this.bread = "";
            this.meat = "";
            this.additionals = [];
        }
    },
    mounted() {
        this.getIngredients();
    },
    components: {
        Message
    },
}
</script>
<style scoped>
    .form {
        max-width: 25rem;
        margin: 0 auto;
    }

    .input-container {
        display: flex;
        flex-direction: column;
        margin-bottom: 1.5rem;
    }

    .label {
        font-weight: bold;
        margin-bottom: .8rem;
        padding: 5px 10px;
        border-left: 4px solid #F29F05;
    }    

    .input {
        padding: .5rem;
        border: solid 1px #47474757;
        border-radius: 5px;
    }

    .additional-container {
        display: flex;
        flex-wrap: wrap;
        margin-bottom: 2rem;
    }

    .checkbox-container {
        display: flex;
        align-items: center;
        width: 50%;
        margin-bottom: 1.25rem;
    }

    .checkbox-container span {
        margin-left: .4rem;
        font-weight: bold;
    }

    .submit-btn {
        width: 100%;
        background-color: #F29F05;
        border: 2px solid #2A2A2A;
        padding: .8rem 0;
        font-size: 1rem;
        font-weight: bold;
        cursor: pointer;
        margin-bottom: 3rem;
    }
</style>
