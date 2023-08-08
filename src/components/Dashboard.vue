<template>
    <div id="container-main">
        <Message :message="msg" v-show="msg" style="margin: auto; width: 50%; margin-bottom: 20px"/>
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
                            <select name="" id="" @change="updatePedido($event, pedido.id)">
                                <option :value="status.tipo" v-for="status in allStatus" :key="status.id" :selected="status.tipo == pedido.status">{{status.tipo}}</option>
                            </select>
                            <button @click="deletePedido(pedido.id)">Cancelar</button>
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
import Message from "./Message.vue"

export default{
    name: "Dashboard",
    data(){
        return{
            pedidos: [],
            allStatus: null,
            msg: null
        }
    },
    methods:{
        async getPedidos(){
            const req = await fetch("http://localhost:3000/burgers");
            const data = await req.json();

            this.pedidos = data;
        },
        async getAllStatus(){
            const req = await fetch('http://localhost:3000/status');
            const data = await req.json();

            this.allStatus = data;
        },
        async deletePedido(pedido_id){
            const req = await fetch(`http://localhost:3000/burgers/${pedido_id}`,{
                method: "delete",
            });
            const pedido = await req.json();

            this.getPedidos();

            this.msg = `Pedido n°${pedido_id} atualizado com sucesso`;

            setTimeout(() => this.msg = "", 2000);

        },
        async updatePedido(event, pedido_id){
            const option = event.target.value;
            const data = JSON.stringify({status: option});

            const req = await fetch(`http://localhost:3000/burgers/${pedido_id}`, {
                method: 'PATCH',
                headers: {'Content-Type' : 'application/json'},
                body: data
            });

            const response = await req.json();

            if(response.status == 'Em produção'){
                this.msg = `O pedido n°${pedido_id} está em produção`;
            }
            else if(response.status == 'Solicitado'){
                this.msg = `O pedido n°${pedido_id} foi solitado`;
            }
            else{
                this.msg = `O pedido n°${pedido_id} foi finalizado`;
            }

            setTimeout(() => this.msg = "", 2000);
        }
    },
    mounted(){
        this.getPedidos();
        this.getAllStatus();
    },
    components: {
        Message
    }
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
