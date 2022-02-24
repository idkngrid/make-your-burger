<template>
    <div class="header">
        <router-link to="/">
            <img :src="logo" :alt="alt" class="header-logo">
        </router-link>
        <nav class="nav" id="nav">
            <router-link to="/">Home</router-link> 
            <router-link to="/pedidos">Pedidos</router-link> 
        </nav> 
    </div>
</template>
<script>
export default {
    name: 'Navbar',
    props: ["logo", "alt"]
}
</script>
<style scoped>
    .header {
        background-color: #2A2A2A;
        padding: 1rem 2rem;
        display: flex;
        justify-content: space-between;
        align-items: center;
    }

    .header-logo {
        width: 35%
    }
    
    .nav a {
        color: #F29F05;
        text-decoration: none;
        margin-left: 2rem;
        font-size: 1.25rem;
        transition: .5s;
    }

    .nav a:hover {
        color: #FFFFFF;
    }
</style>