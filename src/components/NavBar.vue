<template>
    <div id="nav"> 
        <router-link to="/">
                    <img :src="logo_src" :alt="logo_name" id="logo">
        </router-link>
        <ul>
            <li>
                 <router-link to="/">Home</router-link>
            </li>
            <li>
                <router-link to="/pedidos">Pedidos</router-link>
            </li>
        </ul>
    </div>
</template>

<script>
export default{
    name: "NavBar",
    props: ['logo_src', 'logo_name'],
}
</script>

<style scoped>
    div#nav{
        background-color: #222;
        display: flex;
        justify-content: space-between;
        padding: 10px 50px;
        align-items: center;
    }
    div#nav img{
        width: 50px;
    }
    div#nav ul{
        display: flex;
        gap: 3rem;
    }
    div#nav ul li{
        list-style: none;
    }
    div#nav ul li a{
        text-decoration: none;
        color: #ffa500;
        font-family: Arial, Helvetica, sans-serif;
        transition: .3s all;
    }
    div#nav ul li a:hover{
        color: #FFF;
    }
</style>
