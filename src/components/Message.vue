<template>
    <div id="message">
        <p>{{message}}</p> 
    </div>
</template>
<script>
export default {
    name: 'Message',
    props: ['message']
}
</script>

<style scoped>
div#message{
  padding: 10px 0;
  background-color: rgb(35, 165, 35);
  border: 1px solid rgb(143, 206, 143);
  border-radius: 10px;
  color: rgb(255, 255, 255);
  text-align: center;
}
</style>
