<template>
    <div>
        <Header/>
            <div class="container izquierda">

                <table class="table table-hover">
                    <thead>
                        <tr>
                            <th scope="col">ID_INSTRUCTOR</th>
                            <th scope="col">NOMBRE</th>
                            <th scope="col">APELLIDO_PATERNO</th>
                            <th scope="col">APELLIDO_MATERNO</th>
                            <th scope="col">RFC</th>
                            <th scope="col">FORMACION</th>
                        </tr>
                    </thead>
                    <tbody>
                        <tr v-for="area in Listaregistros" :key="area.ID_INSTRUCTOR" v-on:click="editar(area.ID_INSTRUCTOR)">
                            <th scope="row">{{ area.ID_INSTRUCTOR }}</th>
                            <td>{{ area.NOMBRE }}</td>
                            <td>{{ area.APELLIDO_PATERNO }}</td>
                            <td>{{ area.APELLIDO_MATERNO }}</td>
                            <td>{{ area.SEXO }}</td>
                            <td>{{ area.RFC }}</td>
                            <td>{{ area.FORMACION }}</td>
                        </tr>
                    </tbody>
                </table>
                <br>
                <button class="btn btn-primary" v-on:click="nuevo()"> Nuevo Registro </button>
            </div>    
        <Footer/>  
    </div>    
</template>

<script>
import Header from '@/components/Header.vue';
import Footer from '@/components/Footer.vue';
import axios from 'axios';

export default{
    name: "Dashboard",
    data(){
        return{
            Listaregistros:null,
            pagina:1
        }
    },
    components: {
        Header,
        Footer
    },
    methods:{
        editar(id){
            this.$router.push('/editar/' + id);
        },
        nuevo(){
            this.$router.push('/nuevo');
        }
    },
    mounted:function(){
        let direccion = "http://apirest-php.com/instructor?page=1" + this.pagina;
        axios.get(direccion).then( data =>{
            this.Listaregistros = data.data;
        });
    }
}
</script>

<style scoped>