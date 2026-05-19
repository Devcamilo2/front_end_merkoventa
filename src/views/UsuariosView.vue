<script>
import FormularioUsuariosComponent from '@/components/FormularioUsuariosComponent.vue';
import TablaUsuariosComponent from '@/components/TablaUsuariosComponent.vue';

export default {

    data (){
        return{
            recargarTabla : false
        };
    },
    name : "UsuariosView",
    components : {
        FormularioUsuariosComponent,
        TablaUsuariosComponent
    },
    methods : {
        async actualizarTabla() {

            this.recargarTabla = !this.recargarTabla;
        },
    },
};
</script>

<template>

    <div class="usuarios">
        <div class="components">
        <FormularioUsuariosComponent @actualizar-tabla="actualizarTabla"/>
        <TablaUsuariosComponent :recargar="recargarTabla"/>
        </div>
    </div>

</template>
<style>
body{
    font-family: Arial, Helvetica, sans-serif;
    background-color: #f4f6f9;
    margin: 0;
    padding: 20px;
}

.usuarios{
    display: flex;
    gap: 30px;
    align-items: flex-start;
    justify-content: center;
    flex-wrap: wrap;
}

.container{
    background-color: white;
    padding: 25px;
    border-radius: 10px;
    box-shadow: 0px 2px 8px rgba(0,0,0,0.1);
    width: 350px;
}

h1 , h2{
    text-align: center;
    margin-bottom: 20px;
    color: #333;
}

.form-group{
    display: flex;
    flex-direction: column;
}

label{
    margin-bottom: 5px;
    font-weight: bold;
    color: #444;
}

input{
    padding: 10px;
    border: 1px solid #ccc;
    border-radius: 6px;
    outline: none;
    transition: 0.2s;
}

input:focus{
    border-color: #4a90e2;
}

button{
    width: 100%;
    padding: 10px;
    margin-top: 10px;
    border: none;
    border-radius: 6px;
    background-color: #4a90e2;
    color: white;
    font-size: 14px;
    cursor: pointer;
    transition: 0.2s;
}

button:hover{
    background-color: #357abd;
}

table{
    width: 100%;
    border-collapse: collapse;
    background-color: white;
    box-shadow: 0px 2px 8px rgba(0,0,0,0.1);
    border-radius: 10px;
    overflow: hidden;
}

thead{
    background-color: #4a90e2;
    color: white;
}

th, td{
    padding: 12px;
    text-align: center;
    border-bottom: 1px solid #ddd;
}

tr:hover{
    background-color: #f5f5f5;
}
</style>