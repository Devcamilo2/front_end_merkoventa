<script>
import FormularioCarritoComponent from '@/components/FormularioCarritoComponent.vue';
import TablaCarritoComponent from '@/components/TablaCarritoComponent.vue';

export default {
    data (){
        return {
            recargarTabla : false
        }
    },
    name : "CarritoView",
    components : {
        FormularioCarritoComponent,
        TablaCarritoComponent
    },
    methods : {
        actualizarTabla (){
            this.recargarTabla = !this.recargarTabla;
        }
    }
}
</script>

<template>
    <div class="carrito">
        <div class="components">
            <FormularioCarritoComponent @actualizar-tabla="actualizarTabla"/>
            <TablaCarritoComponent :recargar="recargarTabla"/>
        </div>
    </div>
</template>

<style>
.carrito{
    width: 90%;
    max-width: 1200px;
    margin: 40px auto;
    padding: 25px;
    background-color: #ffffff;
    border-radius: 12px;
    box-shadow: 0px 4px 12px rgba(0,0,0,0.1);
}

.components{
    display: flex;
    gap: 30px;
    align-items: flex-start;
    justify-content: space-between;
    flex-wrap: wrap;
}

.components > *{
    flex: 1;
    min-width: 320px;
    background-color: #f8fbff;
    padding: 20px;
    border-radius: 10px;
    border: 1px solid #dbe9f6;
}

h1{
    text-align: center;
    color: #1565c0;
    margin-bottom: 20px;
    font-size: 28px;
}

table{
    width: 100%;
    border-collapse: collapse;
    margin-top: 15px;
    overflow: hidden;
    border-radius: 8px;
}

thead{
    background-color: #1565c0;
    color: white;
}

th,
td{
    padding: 12px;
    text-align: center;
    border-bottom: 1px solid #ddd;
}

tbody tr:nth-child(even){
    background-color: #f5f9ff;
}

tbody tr:hover{
    background-color: #e3f2fd;
    transition: 0.2s;
}

button{
    background-color: #1565c0;
    color: white;
    border: none;
    padding: 10px 15px;
    border-radius: 6px;
    cursor: pointer;
    font-size: 14px;
    transition: 0.3s;
}

button:hover{
    background-color: #0d47a1;
}
</style>