<template>
    <div class="message-container">
        <p>{{ msg }}</p>
    </div>
</template>
<script>
export default {
    name: "Message",
    props: {
        msg: String
    }
}
</script>
<style scoped>
    .message-container {
        color: #004085;
        background-color: #CCE5FF;
        border: 2px solid #88DAFF;
        border-radius: 5px;
        padding: .8rem;
        max-width: 25rem;
        margin: 2rem auto;
    }
</style>