<script>
    import axios from "axios";

    export default{
        data (){
            return{
                carritos : []
            }
        },
        methods : {
            listarCarritos (){
                axios.get("http://localhost:8080/carritos/listarcarrito")
                .then((response) =>{
                    this.carritos = response.data;

                })
                .catch((error)=>{
                    console.error("Fallo al listar" , error)
                });
            },
        eliminarProductos (id){
            axios.delete("http://localhost:8080/carritos/" + id)
            .then(()=>{
                alert("Producto eliminado");
                this.listarCarritos();
            })
            .catch((error)=>{
                console.error(error);
                alert("Eliminación fallida")
            });
        },
    },
    mounted (){
            this.listarCarritos();
        },
        props : {
            recargar : Boolean
        },
        watch : {
            recargar (){
                this.listarCarritos();
            }
        }
};
</script>

<template>

    <div>
        <h1>Carrito</h1>
        <table>
            <thead>
                <tr>
                    <th>Nombre del producto</th>
                    <th>Precio del producto</th>
                    <th>Cantidad del producto</th>
                    <th>Subtotal</th>
                    <th>Acciones</th>
                </tr>
            </thead>

            <tbody>
                <tr v-for="carrito in carritos" :key="carrito.id">
                    <td>{{ carrito.nombreProducto }}</td>
                    <td>{{ carrito.precioProducto }}</td>
                    <td>{{ carrito.cantidadProducto }}</td>
                    <td>{{ carrito.subtotal }}</td>
                    <td><button @click="eliminarProductos(carrito.id)">Eliminar</button></td>
                </tr>
            </tbody>
        </table>
    </div>  
</template>

<style></style>