<template>
    <div id="app">
        <div class="row mt-5 ml-3">
            <div class="col-sm-4">
                <form @submit.prevent="addFeria">
                    <div class="form-group">
                        <input v-model='newFeria.nombre' type="text" class="form-control" placeholder="Nombre empresa">
                    </div>
                    <div class="form-group">
                        <input v-model='newFeria.fecha' type="text" class="form-control" placeholder="Fecha">
                    </div>
                    <div class="form-group">
                        <input v-model='newFeria.link' type="text" class="form-control" placeholder="Link reunion">
                    </div>
                    <button type="submit" class="btn btn-primary btn-block"> 
                        Guardar
                    </button>
                    <button v-on:click="prueba">
                        Prueba
                    </button>
                </form>
            </div>
            
            <div class="col-sm-7">
                <div class="card">
                    <div class="card-body">
                        <h5 class="card-title">Card title</h5>
                        <table class="table table-striped table-dark">
                            <thead>
                                <tr>
                                    <th>Empresa</th>
                                    <th>Fecha</th>
                                    <th>Link</th>
                                </tr>
                            </thead>
                            <tbody>
                                <tr v-for="f in ferias" v-bind:key="f.key">
                                    <td>{{f.nombre}}</td>
                                    <td>{{f.fecha}}</td>
                                    <td>{{f.link}}</td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>
        </div>
    </div>
    
</template>


<script>
import Firebase from 'firebase';
import config from '@/config';
var app = Firebase.initializeApp(config);
var db = app.database();
var feriaRef = db.ref('stands');


export default {
    name: 'App',   
    data(){
        return {
            ferias: {},
            newFeria:{
                nombre: '',
                fecha: '',
                link: ''
            }
        }
    },
    firebase: {
    ferias: feriaRef
    },
    methods:{
        addFeria(){
            feriaRef.push(this.newFeria)
            this.newFeria.nombre = ''
            this.newFeria.fecha = ''
            this.newFeria.link = ''
        },
        prueba(){
            console.log(this.ferias)
        }
    }
}
</script>

<style scoped>
nav a{
    text-decoration: none;
}
</style>