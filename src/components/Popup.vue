<template>
   <v-dialog max-width="600px" v-model="modal">
       <template v-slot:activator="{ on }">
           <v-btn flat class="success" dark v-on="on">
               Add new project
           </v-btn>
       </template>
       <v-card>
           <v-card-title >
               <h2>Add a new project</h2>
           </v-card-title>
           <v-card-text>
               <v-form class="px-3" ref="form">
                   <v-text-field label="Title" v-model="title" prepend-icon="folder" :rules="inputRules"></v-text-field>
                   <v-textarea label="Content" v-model="content" prepend-icon="edit" :rules="inputRules"></v-textarea>
                   <v-menu>
                       <template v-slot:activator="{ on }">
                           <v-text-field v-bind:value="formattedDate"
                                         label="Due date"
                                         prepend-icon="date_range"
                                         readonly
                                         v-on="on"
                                         :rules="inputRules">
                           </v-text-field>
                       </template>
                       <v-date-picker v-model="due" @input="menu2 = false"></v-date-picker>
                   </v-menu>
                   <v-btn flat class="success mx-0 mt-3"
                          v-on:click.prevent="submit"
                          :loading="loading"
                          :disabled="loading">Add Project</v-btn>
               </v-form>
           </v-card-text>
       </v-card>
   </v-dialog>
</template>

<script>
    import format from 'date-fns/format'
    import db from '../firebase/index'
    export default {
        name: "Popup",
        data(){
            return {
                title:'',
                content:'',
                due:null,
                inputRules:[
                    v=>v.length>=3 || 'Minimum length is 3 characters'
                ],
                loading:false,
                modal:false
            }
        },
        methods:{
            submit(){
                if(this.$refs.form.validate()){
                    this.loading=true;
                    const project={
                        title:this.title,
                        content:this.content,
                        duedate:format(this.due, 'Do MMM YYYY'),
                        person:'Aman',
                        state:'ongoing'
                    }

                    db.collection('project-management-vuetify').add(project).then(res=>{
                        console.log(res);
                        this.loading=false;
                        this.modal=false;
                    })
                }

            }
        },
        computed:{
            formattedDate(){
                return this.due? format(this.due, 'Do MMM YYYY'):'';
            }
        }
    }
</script>

<style scoped>

</style>
