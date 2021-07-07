<template>
    <div>
        <Header />
            <div class="container">
                <form action="" class="form-horizontal">
                    <div class="form-group left row">
                        <label for="" class="control-label col.sm-2">Nombre</label>
                        <div class="col-sm-10">
                            <input type="text" class="form-control" name="NOMBRE" id="NOMBRE" v-model="form.NOMBRE">
                            <input type="text" class="form-control" name="APELLIDO_PATERNO" id="APELLIDO_PATERNO" v-model="form.APELLIDO_PATERNO">
                            <input type="text" class="form-control" name="APELLIDO_MATERNO" id="APELLIDO_MATERNO" v-model="form.APELLIDO_MATERNO">
                            <input type="text" class="form-control" name="SEXO" id="SEXO" v-model="form.SEXO">
                            <input type="text" class="form-control" name="RFC" id="RFC" v-model="form.RFC">
                            <input type="text" class="form-control" name="FORMACION" id="FORMACION" v-model="form.FORMACION">
                        </div>
                        <div class="form-group">
                            <button type="button" class="btn btn-primary" v-on:click="editar()">Editar</button>
                            <button type="button" class="btn btn-danger margen" v-on:click="eliminar()">Eliminar</button>
                            <button type="button" class="btn btn-dark margen" v-on:click="salir()">Salir</button>
                        </div>
                    </div>
                </form>
            </div>
        <Footer />
    </div>
</template>

<script>
import Header from '@/components/Header.vue';
import Footer from '@/components/Footer.vue';
import axios from 'axios';

export default{
    name:"Editar",
    components:{
        Header, 
        Footer
    },
    data:function(){
        return{
            
            form:{
                "ID_INSTRUCTOR" : "",
                "NOMBRE" : "",
                "APELLIDO_PATERNO" : "",
                "APELLIDO_MATERNO" : "",
                "SEXO" : "",
                "RFC" : "",
                "FORMACION" : ""
                }
        }
    },

    methods:{
        editar(){
            axios.put("http://apirest-php.com/instructor",this.form)
            .then( data =>{
                console.log(data);
            })
        },
        salir(){
            this.$router.push("/dashboard");
        },
        eliminar(){
            var enviar = {
                "ID_INSTRUCTOR" : this.form.ID_INSTRUCTOR  
            };
            axios.delete("http://apirest-php.com/instructor", { headers : enviar})
            .then( datos =>{
                console.log(datos);
                this.$router.push("/dashboard");
             });
        }
    },

    mounted:function(){
        this.form.ID_AREA = this.$route.params.ID_AREA;
        axios.get("http://TU DOMINIO/instructor?id="+ this.form.ID_INSTRUCTOR)
        
        .then( datos =>{
            this.form.NOMBRE = datos.data.NOMBRE;
            this.form.APELLIDO_PATERNO = datos.data.APELLIDO_PATERNO;
            this.form.APELLIDO_MATERNO = datos.data.APELLIDO_MATERNO;
            this.form.SEXO = datos.data.SEXO;
            this.form.RFC = datos.data.RFC;
            this.form.FORMACION = datos.data.FORMACION;

            
            console.log(this.form);
        })
    }
}

</script>

<style scoped> 
.left{
    text-align: left;
}
</style>