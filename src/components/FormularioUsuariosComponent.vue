<script>

import axios from "axios";

export default {

    data(){

        return{

            codigo : 0,

            nombreUsuario : "",
            apellidoUsuario : "",
            usuarioContrasena : "",
            edadUsuario : 0
        };
    },

    methods : {

        guardar (){
            axios.post("http://localhost:8080/usuarios" , {
                nombreUsuario : this.nombreUsuario,
                apellidoUsuario : this.apellidoUsuario,
                usuarioContrasena : this.usuarioContrasena,
                edadUsuario : this.edadUsuario

            })

            .then((response)=>{
                console.log(response.data);
                alert("Usuario registrado");
                this.limpiarFormulario();
                this.$emit("actualizar-tabla");
            })
            .catch((error)=>{
                console.error(error);
                alert("Error al registrar usuario");
            });
        },

        login (){
            axios.post("http://localhost:8080/usuarios/login" , {
                nombreUsuario : this.nombreUsuario,
                usuarioContrasena : this.usuarioContrasena
            })

            .then((response)=>{
                alert(response.data);
                console.log(response.data);
            })

            .catch((error)=>{
                console.error(error);
                alert("Error en login");
            });
        },

        consultar (){

            axios.get("http://localhost:8080/usuarios/" + this.codigo)
            .then((response)=>{
                this.nombreUsuario = response.data.nombreUsuario;
                this.apellidoUsuario = response.data.apellidoUsuario;
                this.edadUsuario = response.data.edadUsuario;
            })

            .catch((error) =>{
                console.error(error);
                alert("Consulta fallida");
            });
        },

        actualizar() {
            axios.put("http://localhost:8080/usuarios/" + this.codigo , {
                nombreUsuario : this.nombreUsuario,
                apellidoUsuario : this.apellidoUsuario,
                usuarioContrasena : this.usuarioContrasena,
                edadUsuario : this.edadUsuario
            })

            .then((response)=>{
                alert("Usuario actualizado");
                console.log(response.data);
            })

            .catch((error)=>{
                console.error(error);
                alert("Actualización fallida");
            });
        },

        eliminar() {
            axios.delete("http://localhost:8080/usuarios/" + this.codigo)
            .then(()=>{
                alert("Usuario eliminado");
                this.limpiarFormulario();
            })
            .catch((error)=>{
                console.error(error);
                alert("Eliminación fallida");
            });
        },

        limpiarFormulario(){
            this.codigo = "";
            this.nombreUsuario = "";
            this.apellidoUsuario = "";
            this.usuarioContrasena = "";
            this.edadUsuario = 0;
        },

        recargarTabla (){
            console.log("Tabla recargada")
        },
    },
};

</script>

<template>

    <div class="container">

        <h1>Formulario usuarios</h1>

        <form action="" id="usuary-form" @submit.prevent="guardar">

            <div class="form-group">
                <label for="nombre">Nombre</label>
                <input type="text" id="nombre" name="nombre" v-model="nombreUsuario" required>
            </div> <br>

            <div class="form-group">
                <label for="apellido">Apellido</label>
                <input type="text" id="apellido" name="apellido" v-model="apellidoUsuario" required>
            </div> <br>

            <div class="form-group">
                <label for="contrasena">Contraseña</label>
                <input type="text" id="contrasena" name="contrasena" v-model="usuarioContrasena" required>
            </div> <br>

            <div class="form-group">
                <label for="edad">Edad</label>
                <input type="number" id="edad" name="edad" v-model="edadUsuario" required>
            </div> <br>

            <div class="form-group">
                <label>ID</label>
                <input type="number" id="codigo" name="codigo" v-model="codigo">
            </div> <br>

            <button type="submit">Guardar</button><br>
            <button type="button" @click="eliminar" >Eliminar</button><br>
            <button type="button" @click="actualizar">Actualizar</button><br>
            <button type="button" @click="consultar">Consultar</button><br>
            <button type="button" @click="login">Login</button>
        </form>

    </div>

</template>

<style></style>