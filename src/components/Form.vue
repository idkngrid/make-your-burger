<template>
    <div>
        <p>componente de mensagem</p>
    </div>
        <form action="#" class="form">
            <div class="input-container">
                <label for="name" class="label">Nome</label>
                <input type="text" id="name" class="input" v-model="name" placeholder="Digite o seu nome">
            </div>
            <div class="input-container">
                <label for="bread" class="label">Escolha o pão: </label>
                <select name="bread" id="bread" class="input" v-model="bread">
                    <option value="">Selecione o seu pão</option>
                    <option value="integral">Integral</option>
                </select>
            </div>
            <div class="input-container">
                <label for="meat" class="label">Escolha a carne do seu Burger: </label>
                <select name="meat" id="meat" class="input" v-model="meat">
                    <option value="">Selecione sua carne</option>
                    <option value="maminha">Maminha</option>
                </select>
            </div>
            <div class="additional-container">
                <label for="additional" class="label additional-label">Selecione os adicionais: </label>
                <div class="checkbox-container">
                    <input type="checkbox" name="additional" id="additional" class="input checkbox" v-model="additional" value="salame">
                    <span>Salame</span>
                </div>
            </div>
            <div>
                <input type="submit" class="submit-btn" value="Criar meu Burger">
            </div>
        </form>
</template>
<script>
export default {
    name: 'Form',
    data() {
        return {

        }
    }
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
        flex-direction: row;
        flex-wrap: wrap;
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

    .submit-btn:hover {
        background-color: transparent;
        border: 2px solid #F29F05;
    }
</style>
