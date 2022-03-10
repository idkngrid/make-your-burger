<template>
    <div class="burger-table">
        <Message :msg="msg" v-show="msg" />
        <div>
            <div class="table-heading">
                <div class="order-id">#: </div>
                <div>Cliente: </div>
                <div>Pão: </div>
                <div>Carne: </div>
                <div>Adicionais: </div>
                <div>Ações: </div>
            </div>
            <div class="table-rows" v-for="burger in burgers" :key="burger.id">
                <div class="order-number">{{ burger.id }}</div>
                <div>{{ burger.name }}</div>
                <div>{{ burger.bread }}</div>
                <div>{{ burger.meat }}</div>
                <div>
                    <ul>
                        <li v-for="(additional, index) in burger.additionals" :key="index">
                            {{ additional }}
                        </li>
                    </ul>
                </div>
                <div>
                    <select name="status" class="order-status" @change="updateBurger($event, burger.id)">
                        <option :value="s.tipo" v-for="s in status" :key="s.id" :selected="burger.status == s.tipo"> 
                            {{ s.tipo }}
                        </option>
                    </select>
                    <button class="delete-btn" @click="deleteBurger(burger.id)">Cancelar</button>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
import Message from './Message.vue'

export default {
    name: "Dashboard",
    data() {
        return {
            burgers: null,
            burger_id: null,
            status: [],
            msg: null
        }
    },
    components: {
        Message
    },
    methods: {
        async getOrders() {
            const req = await fetch("http://localhost:3000/burgers");

            const data = await req.json();
            this.burgers = data;

            // resgatar os status
            this.getStatus();
        },
        async getStatus() {
            const req = await fetch("http://localhost:3000/status");

            const data = await req.json();
            this.status = data;
        },
        async deleteBurger(id) {
            
            const req = await fetch(`http://localhost:3000/burgers/${id}`, {
                method: "DELETE"
            });

            const res = await req.json();

            // msg de sistema
            this.msg = `Pedido removido com sucesso!`

            // limpar msg
            setTimeout(() => this.msg = "", 3000);

            this.getOrders();
        },
        async updateBurger(event, id) {

            const option = event.target.value;
            const dataJson = JSON.stringify({status: option});

            const req = await fetch(`http://localhost:3000/burgers/${id}`, {
            method: "PATCH",
            headers: { "Content-Type" : "application/json" },
            body: dataJson
            });

            const res = await req.json()

            // msg de sistema
            this.msg = `O pedido nº ${res.id} foi atualizado para ${res.status}!`

            // limpar msg
            setTimeout(() => this.msg = "", 3000);
        }
    },
    mounted() {
        this.getOrders();
    }
}
</script>
<style scoped>
    .burger-table {
        max-width: 75rem;
        margin: 0 auto;
    }

    .table-heading, 
    .table-rows {
        display: flex;
        flex-wrap: wrap;
    }

    .table-heading {
        font-weight: bold;
        padding: 1rem;
        border-bottom: 3px solid #2A2A2A;
    }

    .table-heading div,
    .table-rows div {
        width: 19%;
    }

    .table-rows {
        width: 100%;
        border-bottom: 1px solid #ccc;
        padding: 1rem;
    }

    .table-heading .order-id,
    .table-rows .order-number {
        width: 5%;
    }

    select {
        padding: .5rem .3rem;
    }

    .delete-btn {
        background-color: #F29F05;
        border: 2px solid #2A2A2A;
        margin-top: .5rem;
        margin-left: .8rem;
        padding: .43rem .3rem;
        font-size: .9rem;
        font-weight: bold;
        cursor: pointer;
        transition: .5s;
    }
</style>