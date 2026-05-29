<script>
    import axios from "axios";

    export default {
        data(){

            return {
                idProducto : 0,
                cantidadProducto : 0
            };
        },
        
        methods : {
            guardar(){
                axios.post("http://localhost:8080/carritos/agregarcarrito" , {
                    idProducto : this.idProducto,
                    cantidadProducto : this.cantidadProducto
                })
                .then((response) => {
                    console.log("Producto registrado con exito" , response.data);
                    alert("Producto registrado");
                    this.idProducto = 0,
                    this.cantidadProducto = 0,
                    this.$emit("actualizar-tabla");
                })
                .catch((error) => {
                    console.error("Error al registrar producto", error);
                });
            },
        }
    };
</script>

<template>
    <div class="container">

        <h1>Formulario carrito</h1>

        <form action="" id="carrito-form" @submit.prevent="guardar">

            <div class="form-group">
                <label for="idProducto">Id del producto</label>
                <input type="number" id="idProducto" name="idProducto" v-model.number="idProducto" required>
            </div> <br>

            <div class="form-group">
                <label for="cantidadProducto">Cantidad del producto</label>
                <input type="number" id="cantidadProducto" name="cantidadProducto" v-model.number="cantidadProducto" required>
            </div> <br>

            <button type="submit">Agregar producto al carrito</button><br>
            <!--<button type="button" @click="eliminar" >Eliminar</button><br>-->
            <!--<button type="button" @click="actualizar">Actualizar</button><br>-->
            <!--<button type="button" @click="consultar">Consultar</button><br>-->
        </form>

    </div>
</template>

<style></style>