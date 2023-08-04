<template>
    <div id="main-banner">
        <h1>Make Your Burguer</h1>
    </div>
</template>

<script>

export default {
    name: "Banner"
}
</script>

<style scoped>
    #main-banner {
        background-image: url('/public/img/burger.jpg');
        background-position: 0 -150px;
        background-size: cover;
        background-attachment: fixed;
        height: 500px;
        display: flex;
        justify-content: center;
        align-items: center;
    }
    h1{
        color: #FFF;
        padding: 10px;
        font-size: 40px;
        text-transform: initial;
    }
</style>