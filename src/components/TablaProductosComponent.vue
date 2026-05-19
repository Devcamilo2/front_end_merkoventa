<script>

    import axios from "axios";

    export default{
        data(){
            return{
            productos : [],
            }
        },
        methods : {
            obtenerProductos() {
                axios.get("http://localhost:8080/productos/listarproductos")
                .then((response)=>{
                    this.productos = response.data;
                })
                .catch((error)=>{
                    alert("Listar fallo" , error)
                });
            },
        },
        mounted() {
            this.obtenerProductos();
        },
        props : {
            recargar : Boolean
        },
        watch : {
            recargar(){
                this.obtenerProductos();
            }
        }
    };

</script>

<template>

    <div>
        <h1>Tabla productos</h1>
        <table>
            <thead>
                <tr>
                    <th>Nombre</th>
                    <th>Codigo</th>
                    <th>Descripción</th>
                    <th>Precio</th>
                    <th>Stock</th>
                    <th>Disponible</th>
                </tr>
            </thead>

            <tbody>
                <tr v-for="producto in productos" :key="producto.codigo">
                    <td>{{ producto.nombre }}</td>
                    <td>{{ producto.codigo }}</td>
                    <td>{{ producto.descripcion }}</td>
                    <td>{{ producto.precio }}</td>
                    <td>{{ producto.stock }}</td>
                    <td>{{ producto.disponible ? "Si" : "No"}}</td>
                </tr>
            </tbody>
        </table>
    </div>  
</template>

<style></style>