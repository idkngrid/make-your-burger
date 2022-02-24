<template>
    <div class="main-banner">
        <h1 class="banner-title">Make Your Burger</h1>
    </div>
</template>
<script>
export default {
    name: 'Banner'
}
</script>
<style scoped>
    .main-banner {
        background: url('/public/img/burger.jpg') no-repeat center/cover;
        margin-bottom: 2rem;
        height: 500px;
        display: flex;
        align-items: center;
    }

    .banner-title {
        color: #1A2026;
        background: #BF5B04;
        padding: 1rem;
        border-radius: 0 33px 33px 0;
    }

    @media(min-width: 1400px) {
        .main-banner { 
            height: 700px;
        }
    }
</style>