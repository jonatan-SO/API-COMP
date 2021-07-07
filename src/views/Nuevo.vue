<template>
    <div>
        <Header />
            <div class="container">
                <form action="" class="form-horizontal">
                    <div class="form-group left row">
                        <label for="" class="control-label col.sm-2">NOMBRE</label>
                        <div class="col-sm-10">
                            <input type="text" class="form-control" name="NOMBRE" id="NOMBRE" v-model="form.NOMBRE">
                            <input type="text" class="form-control" name="APELLIDO_PATERNO" id="APELLIDO_PATERNO" v-model="form.APELLIDO_PATERNO">
                            <input type="text" class="form-control" name="APELLIDO_MATERNO" id="APELLIDO_MATERNO" v-model="form.APELLIDO_MATERNO">
                            <input type="text" class="form-control" name="SEXO" id="SEXO" v-model="form.SEXO">
                            <input type="text" class="form-control" name="RFC" id="RFC" v-model="form.RFC">
                            <input type="text" class="form-control" name="FORMACION" id="FORMACION" v-model="form.FORMACION">
                        </div>
                        <div class="form-group">
                            <button type="button" class="btn btn-primary" v-on:click="guardar()">Guardar</button>
                            <button type="button" class="btn btn-dark margen" v-on:click="salir()">Salir</button>
                        </div>
                    </div>
                </form>
            </div>
        <Footer />
    </div>
</template>

<script>
import Header from '@/components/Header.vue/'
import Footer from '@/components/Footer.vue/'
import axios from 'axios'

export default{
    name:"Nuevo",
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

    components:{
        Header,
        Footer
    },
    methods:{
        guardar(){
            
            axios.post("http://apirest-php.com/instructor", this.form)
            .then( data =>{
                console.log(data);
                this.makeToast("Hecho","area creada", "success");
                this.$router.push("/dashboard");
            }).catch( e =>{
                console.log(e);
                this.makeToast("Error","Error Al Guardar", "error");
            })
        },
        salir(){
            this.$router.push("/dashboard");
        },
        makeToast(titulo,texto,tipo) {
            this.toastCount++
            this.$bvToast.toast(texto, {
            title: titulo,
            variant: tipo,
            autoHideDelay: 5000,
            appendToast: true
            })
        }
    }
}

</script>

<style scoped>
.left{
    text-align: left;
}
</style>