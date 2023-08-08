<template>
    <div id="container-main">
        <table v-if="pedidos.length > 0">
            <thead>
                <tr>
                    <th>#</th>
                    <th>Cliente</th>
                    <th>Pão</th>
                    <th>Carne</th>
                    <th>Opcionais</th>
                    <th>Ações</th>
                </tr>
            </thead>
            <tbody v-for="pedido in pedidos" :key="pedido.id">
                <tr>
                    <td>{{pedido.id}}</td>
                    <td>{{pedido.nome}}</td>
                    <td>{{pedido.pao}}</td>
                    <td>{{pedido.carne}}</td>
                    <td>
                        <ul>
                            <li v-for="opcional in pedido.opcionais" :key="opcional.id">{{opcional}}</li>
                        </ul>
                    </td>
                    <td>
                        <div id="actions">
                            <select name="" id="">
                                <option value="Solicitado">Solicitado</option>
                                <option value="Em producao" selected>Em produção</option>
                                <option value="Finalizado">Finalizado</option>
                            </select>
                            <button>Cancelar</button>
                        </div>
                    </td>
                </tr>
            </tbody>
        </table>
        <div v-else>
            <h3>Não há pedidos no momento</h3>
        </div>
    </div>
</template>
<script>
export default{
    name: "Dashboard",
    data(){
        return{
            pedidos: [],
        }
    },
    methods:{
        async getPedidos(){
            const req = await fetch("http://localhost:3000/burgers");
            const data = await req.json();

            this.pedidos = data;
        }
    },
    mounted(){
        this.getPedidos();
    },
}
</script>
<style scoped>
table{
    border-collapse: collapse;
}
td,th{
    border-bottom: 2px solid #808080;
    padding: 10px 50px;
}
th{
    border-bottom: 2px solid #000;
    padding: 20px 50px;
}
#actions{
    display: flex;
    flex-wrap: wrap;
    gap: 10px;
}
select{
    padding: 10px;
}
button{
    background-color: #222;
    color:#fcba03;
    font-weight: bold;
    border: 2px solid #222;
    padding: 10px;
    font-size: 16px;
    margin: 0 auto;
    cursor: pointer;
    transition: .5s;
}

button:hover {
    background-color: transparent;
    color: #222;
}

</style>
