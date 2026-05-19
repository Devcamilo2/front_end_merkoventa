<script>

import axios from "axios";

export default {

    data(){

        return{

            usuarios : [],
        }
    },

    methods : {

        obtenerUsuarios() {

            axios.get("http://localhost:8080/usuarios")
            .then((response)=>{
                this.usuarios = response.data;
            })
            .catch((error)=>{
                console.error(error);
                alert("Listar falló");
            })
        }
    },

    mounted() {
        this.obtenerUsuarios();
    },

    props : {
        recargar : Boolean
    },

    watch : {
        recargar(){
            this.obtenerUsuarios();
        }
    }
};

</script>

<template>
    <div>
        <h1>Tabla usuarios</h1>
        <table border="1">
            <thead>
                <tr>
                    <th>ID</th>
                    <th>Nombre</th>
                    <th>Apellido</th>
                    <th>Edad</th>
                </tr>
            </thead>

            <tbody>
                <tr v-for="usuario in usuarios" :key="usuario.id">
                    <td>{{ usuario.id }}</td>
                    <td>{{ usuario.nombreUsuario }}</td>
                    <td>{{ usuario.apellidoUsuario }}</td>
                    <td>{{ usuario.edadUsuario }}</td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<style></style>