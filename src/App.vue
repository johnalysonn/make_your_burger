<template>
  <div>
    <Navbar :logo_src="src" :logo_name="name"/>
    <router-view/>
    <Footer/>
  </div>
</template>

<script>
import Navbar from './components/NavBar.vue'
import Footer from './components/Footer.vue'

export default{
  name: "App",
  components: {
    Navbar,
    Footer
  },
  data(){
    return {
      src: "/img/logo.png",
      name: "Make_Your_Burguer"
    }
  }
}
</script>

<style>
  *{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: Helvetica, sans-serif;
  }

  .main-container{
    min-height: 250px;
    padding: 50px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }
  h1{
    margin-bottom: 50px;
    text-align: center;
    text-transform: uppercase;
  }
</style>
