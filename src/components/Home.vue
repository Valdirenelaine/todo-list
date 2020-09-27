<template>
    <div>
        <v-row justify="center" class="my-5" v-if="loading">
            <v-col cols="auto">
                <v-progress-circular
                    indeterminate
                    color="primary">
                </v-progress-circular>

            </v-col>    
        </v-row>    
        <v-row v-else>
            <v-col v-for="item in tarefas" :key="item.titulo" cols="12" nd="6" lg="3" xl="2"> 
                <v-card>
                  <v-card-title>{{item.titulo}}</v-card-title>
                  <v-card-text>{{item.descricao}}</v-card-text>
               </v-card>
            </v-col>
        </v-row>

        <v-speed-dial absolute bottom right>
              <template v-slot:activator>
                 <v-btn color="primary" dark fab @click="novaTarefa">
                     <v-icon>mdi-plus</v-icon>
                </v-btn>
            </template>
        </v-speed-dial>

        <v-dialog v-model="dialog"> 
            <v-card>
                <v-card-title>Nova Tarefa</v-card-title>
                <v-card-text>
                    <v-form>
                        <v-row dense>
                            <v-col cols ="12"> 
                                <v-text-field v-model="tarefa.titulo" type="text" label="Título" outlined></v-text-field>
                            </v-col>
                            <v-col cols ="12"> 
                                <v-text-field  v-model="tarefa.descricao"  type="text" label="Descrição" outlined></v-text-field>
                            </v-col>
                            <v-col cols ="12"> 
                                <v-btn color="primary" class="elevation-0" block rounded @click="salvar">Salvar</v-btn>
                            </v-col>
                        </v-row>
                    </v-form>
                </v-card-text>
            </v-card>
        </v-dialog>

    </div>
</template>

<script>
import axios from 'axios'
export default {
    data(){
        return {
            loading: true,
            dialog: false,
            tarefa: {},
            tarefas: []
         }
    },
  methods: {
      novaTarefa(){
          this.dialog = true
      },
    async  salvar(){
          await axios.post('http://localhost:3000/tarefas', this.tarefa)
          this.buscarTarefas()
          this.tarefa={}
          this.dialog = false
      },
      async buscarTarefas(){
         this.loading = true 
         const resposta = await axios.get('http://localhost:3000/tarefas')
         this.tarefas = resposta.data
         this.loading = false
      }
  } ,
  mounted(){
      this.buscarTarefas()
  }
}
</script>