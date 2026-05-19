<script>

import axios from "axios";

export default {
    data(){

        return{
            codigo : 0,
            nombre : "",
            descripcion : "",
            precio : 0,
            stock : 0,
            disponible : false
        };
    },
    methods : {
        guardar (){
            axios.post("http://localhost:8080/productos" , {
                codigo : this.codigo,
                nombre : this.nombre,
                descripcion : this.descripcion,
                precio : this.precio,
                stock : this.stock,
                disponible : this.disponible
            })
            .then((response)=>{
                console.log("Producto registrado con exito" , response.data);
                alert("Producto registrado");
                this.codigo = "";
                this.nombre = "";
                this.descripcion = "";
                this.precio = "";
                this.stock = "";
                this.disponible = "";
                this.$emit("actualizar-tabla");
            })
            .catch((error)=>{
                console.error("Error al registrar producto" , error);
            });
        },

        consultar (){
            axios.get("http://localhost:8080/productos/" + this.codigo)
            .then((response)=>{
                this.nombre = response.data.nombre;
                this.descripcion = response.data.descripcion;
                this.precio = response.data.precio;
                this.stock = response.data.stock;
                this.disponible = response.data.disponible;
            })
            .catch((error) =>{
                alert("Consuta fallida" , error)
            });
        },

        actualizar() {
            axios.put("http://localhost:8080/productos/actualizarproducto/" + this.codigo , {
                codigo : this.codigo,
                nombre : this.nombre,
                descripcion : this.descripcion,
                precio : this.precio,
                stock : this.stock,
                disponible : this.disponible
            })
            .then((response)=>{
                alert("Producto actualizado con exito" , response.data);
            })
            .catch((error)=>{
                alert("Actualización fallida" , error);
                console.error(error);
            });
        },

        eliminar() {
            axios.delete("http://localhost:8080/productos/" + this.codigo)
            .then(()=>{
                alert("Producto eliminado con exito");
            })
            .catch((error)=>{
                alert("Eliminación fallida" , error);
            })
        },
    },
};

</script>

<template>

    <div class="container">

        <h1>Formulario productos</h1>

        <form action="" id="client-form" @submit.prevent="guardar">

            <div class="form-group">
                <label for="nombre">Nombre</label>
                <input type="text" id="nombre" name="nombre" v-model="nombre" required>
            </div> <br>

            <div class="form-group">
                <label for="codigo">Codigo</label>
                <input type="number" id="codigo" name="codigo" v-model="codigo" required>
            </div> <br>

            <div class="form-group">
                <label for="descripcion">Descripción</label>
                <input type="text" id="descripcion" name="descripcion" v-model="descripcion" required>
            </div> <br>

            <div class="form-group">
                <label for="precio">Precio</label>
                <input type="number" id="precio" name="precio" v-model="precio" required>
            </div> <br>

            <div class="form-group">
                <label for="stock">Stock</label>
                <input type="number" id="stock" name="stock" v-model="stock" required>
            </div> <br>

            <h2>Disponible</h2>
            <select v-model="disponible">
                <option :value="true">Si</option>
                <option :value="false">No</option>
            </select>

            <button type="submit">Guardar</button><br>
            <button type="button" @click="eliminar" >Eliminar</button><br>
            <button type="button" @click="actualizar">Actualizar</button><br>
            <button type="button" @click="consultar">Consultar</button><br>
        </form>

    </div>

</template>

<style></style>