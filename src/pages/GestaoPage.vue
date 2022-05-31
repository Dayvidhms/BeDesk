<template>
<Header>
    <body id="body">
        <div class="head">
            <div class="other-user">
                <q-btn rounded color="primary" label="Acessar com outro usuário" />
            </div>
        </div>
        <div class="panel-actions">
            <div class="chamados">
                <q-table
                    :columns="columns"
                    :rows="chamadosdata"
                    row-key="name"
                    dark
                    bordered
                    separator="cell"
                    no-data-label="Nenhum chamado cadastrado."
                    :filter="filter"
                    @row-click="open"
                    no-results-label="Nenhum chamado encontrado com os parâmetros selecionados.">
                    <template v-slot:top-right>
                        <q-input dark borderless dense debounce="300" v-model="filter" placeholder="Pesquisar">
                        <template v-slot:append>
                            <q-icon name="search" />
                        </template>
                        </q-input>
                    </template>
                    <template>
                        <q-tr :props="props">
                            <q-td key="codigo" :props="props">
                                {{ props.row.codigo }}
                            </q-td>
                            <q-td key="data" :props="props">
                                {{ props.row.data }}
                            </q-td>
                            <q-td key="descricao" :props="props">
                                {{ props.row.descricao }}
                            </q-td>
                            <q-td key="user" :props="props">
                                {{ props.row.usuario }}
                            </q-td>
                            <q-td key="prioridade" :props="props">
                                {{ props.row.prioridade }}
                            </q-td>
                            <q-td key="nivel" :props="props">
                                {{ props.row.nivel }}
                            </q-td>
                            <q-td key="status" :props="props">
                                {{ props.row.status }}
                            </q-td>
                        </q-tr>
                    </template>
                </q-table>
                <div class="btn-actions">
                    <q-btn glossy push color="positive" icon="add" label="Adicionar" @click="open"/>
                    <q-btn glossy push color="negative" icon="remove" label="Excluir" />
                    <q-btn glossy push color="warning" icon="edit" label="Alterar" />
                </div>
                <div class="modal">
                    <q-dialog
                        v-model="addModal"
                        full-height
                        full-width
                        transition-duration="700"
                        transition-hide="fade"
                        transition-show="fade"

                        >
                        <q-card class="modal-content column full-height ">
                            <q-card-section>
                            <div class="text-h6 modal-title">Cadastrar Incidente</div>
                            </q-card-section>

                            <q-card-section class="col q-pt-none">
                                <div class="header-content">
                                    <div class="chamados">
                                        <p>Chamado:</p>
                                        <q-input outlined v-model="chamado" label="Chamado" />
                                    </div>
                                    <div class="datas">
                                        <p>Data:</p>
                                        <q-input outlined v-model="dataHoje" readonly/>
                                    </div>
                                    <div class="users">
                                        <p>Usuário:</p>
                                        <q-input outlined v-model="usuario" readonly />
                                    </div>
                                </div>
                                <div class="body-content">
                                    <div class="area">
                                        <p>Área:</p>
                                        <q-select outlined v-model="area" :options="optionsArea" label="Área" />
                                    </div>
                                    <div class="status">
                                        <p>Status:</p>
                                        <q-select outlined v-model="status" :options="optionsStatus" label="Status" />
                                    </div>
                                    <div class="nivel">
                                        <p>Nível:</p>
                                        <q-select outlined v-model="nivel" :options="optionsNivel" label="Nível" />
                                    </div>
                                </div>
                                <div class="descript">
                                    <p>Descrição:</p>
                                    <q-input
                                        bottom-slots
                                        v-model="description"
                                        label="Descrição"
                                        counter
                                        maxlength="150"
                                        filled
                                        autogrow
                                    >
                                        <template v-slot:hint>
                                        Caracteres
                                        </template>
                                    </q-input>
                                </div>

                                <div class="actions">
                                    <p>Ações:</p>
                                    <div class="table-action">
                                        <q-table
                                        :rows="actionRows"
                                        :columns="actionColumns"
                                        row-key="name"
                                        :rows-per-page-options="maxRows"
                                        bordered
                                        separator="cell"
                                        no-data-label="Nenhum chamado cadastrado."
                                        :filter="filter"
                                        no-results-label="Nenhum chamado encontrado com os parâmetros selecionados."
                                        />
                                    </div>
                                </div>

                                <div class="uploadDoc">
                                    <p>Anexos:</p>
                                    <q-input
                                        @update:model-value="val => { files = val }"
                                        multiple
                                        filled
                                        dense
                                        type="file"
                                    />
                                </div>

                            </q-card-section>

                            <q-card-actions align="right" class="bg-white text-primary">
                            <q-btn label="Cancelar" v-close-popup />
                            <q-btn label="Gravar" v-close-popup @click.prevent="gravarChamado" />
                            </q-card-actions>
                        </q-card>
                    </q-dialog>
                </div>
            </div>
        </div>
    </body>
</Header>
<Footer>

</Footer>
</template>

<script>
import { useRouter } from 'vue-router';
import { defineComponent, ref } from 'vue';
import Header from '../components/Header.vue';
import Footer from '../components/Footer.vue';

import axios from 'axios';
import swal from 'sweetalert';

    const actionColumns = [
        { name: 'data', align: 'center', label: 'Data', field: 'data', sortable: true, sort: (a, b) => parseInt(a, 10) - parseInt(b, 10)},
        { name: 'descricao', align: 'center', label: 'Descrição', field: 'descricao', sortable: true, sort: (a, b) => parseInt(a, 10) - parseInt(b, 10)  },
        { name: 'usuario', align: 'center', label: 'Usuário', field: 'usuario', sortable: true, sort: (a, b) => parseInt(a, 10) - parseInt(b, 10) },
    ]

    let action;

    const actionRows = [
        {
            data: '25/05/2022',
            descricao: 'Problema para acessar a internet',
            usuario: 'Gabriel',
        },
        {
            data: '25/05/2022',
            descricao: 'Problema para acessar a internet',
            usuario: 'Gabriel',
        },
        {
            data: '25/05/2022',
            descricao: 'Problema para acessar a internet',
            usuario: 'Gabriel',
        },
        {
            data: '25/05/2022',
            descricao: 'Problema para acessar a internet',
            usuario: 'Gabriel',
        },
    ]

export default defineComponent({
  data(){
    return {
      columns: [

        { name: 'codigo', align: 'center', label: 'Código', field: 'codigo', sortable: true, sort: (a, b) => parseInt(a, 10) - parseInt(b, 10)},
        { name: 'data', align: 'center', label: 'Data', field: 'data' },
        { name: 'descricao', align: 'center', label: 'Descrição', field: 'descricao' },
        { name: 'usuario', align: 'center', label: 'Usuário', field: row => row.User.user },
        { name: 'prioridade', align: 'center', label: 'Prioridade', field: 'prioridade', sortable: true, sort: (a, b) => parseInt(a, 10) - parseInt(b, 10)  },
        { name: 'nivel', align: 'center', label: 'Nível', field: 'nivel', sortable: true, sort: (a, b) => parseInt(a, 10) - parseInt(b, 10) },
        { name: 'status', align: 'center', label: 'Status', field: 'status'},

      ],

      chamadosdata: []
    }
  },


  name: 'GestaoPage',
  components: {
    Header,
    Footer,
  },

  setup () {

    const router = useRouter();
    const chamado = ref("");
    const dataHoje = ref("");
    const usuario = ref("");
    const area = ref("");
    const status = ref("");
    const nivel = ref("");
    const description = ref("");
    const id = ref(0);

    let dataObjeto;
    let oldStatus;

    const redirectTo = (view) => {
      router.push({ path : view});
    };

    return {
      redirectTo,
      actionColumns,
      actionRows,
      filter: ref(''),
      addModal: ref(false),
      description: ref(''),
      file: ref(null),
      maxRows: [2],
      chamado,
      dataHoje,
      dataObjeto,
      area,
      usuario,
      status,
      nivel,
      id,
      description,
      optionsArea:[{label:'Teste', value: 0}],
      optionsNivel:[{label:'Teste', value: 0}],
      optionsStatus:[{label:'Criado', value: 0}, {label:'Em Andamento', value: 1}, {label:'Paralisado', value: 2}, {label:'Concluído', value: 3}],
    }
  },
  created(){
    if(this.getCookie('user') == null){
      swal({
          title: "Usuário desconectado",
          text: "Você será redirecionado para a tela de login.",
          icon: "error",
          button: "Ok",
        }).then(this.redirectTo('./login'))
    };
  },
  mounted(){
    if(this.getCookie('user') != null)
      this.getChamados();
  },
  methods:{

      getChamados(){

        const tipo = this.getCookie('tipo');

        if(tipo==2){

        axios.get("http://127.0.0.1:3000/chamado/userChamados", {params:{userId: this.getCookie('user')}})
        .then((res) => {
          let result = res.data;
          this.chamadosdata = result;
        })
        .catch((err) => {
          console.log(err)
        });
      }else if(tipo==1){
        axios.get("http://127.0.0.1:3000/chamado/chamados")
        .then((res)=>{
          let result = res.data;
          this.chamadosdata = result;
        })
        .catch((err) => {
          console.log(err);
        });
      }
      },

      getCookie(cName){
      const name = cName + "=";
      const cDecoded = decodeURIComponent(document.cookie); //to be careful
      const cArr = cDecoded.split('; ');
      let res;
      cArr.forEach(val => {
        if (val.indexOf(name) === 0) res = val.substring(name.length);
      })
      return res;
    },

    gravarChamado(){
      const postData = {chamado: this.chamado, date: this.dataObjeto, usuario: this.getCookie('user'), area: this.area.value, status: this.status.value, nivel: this.nivel.value, descricao: this.description};

      if(this.action == 1){
      axios.post("http://127.0.0.1:3000/chamado/inserir", postData)
        .then(res=>{
          if(res.data == true){
            swal({
              title: "Chamado aberto com sucesso.",
              text: "Chamado aberto com sucesso.",
              icon: "success",
              button: "Ok",
            }).then(window.location.reload())
          }else{
            swal({
              title: "Falha ao abrir o chamado.",
              text: "Houve algum erro ao registrar o chamado.",
              icon: "error",
              button: "Ok",
            });
          }
        });
      }else if(this.action == 0){
        let statusChanged = false;

        if(this.oldStatus.value != this.status.value){
          statusChanged = true;
        }

        const postData = {id: this.id, chamado: this.chamado, date: this.dataObjeto, usuario: this.getCookie('user'), area: this.area.value, status: this.status.value, nivel: this.nivel.value, descricao: this.description, statusChanged: statusChanged};

        axios.post("http://127.0.0.1:3000/chamado/atualizar", postData)
        .then(
          res =>{
            console.log(res.data);
            if(res.data==true){
              swal({
              title: "Chamado alterado com sucesso.",
              text: "Chamado alterado com sucesso.",
              icon: "success",
              button: "Ok",
            }).then(window.location.reload());
            }else{
              swal({
              title: "Falha ao alterar o chamado.",
              text: "Houve algum erro ao alterar o chamado.",
              icon: "error",
              button: "Ok",
            });
            }
          }
        )
      }
    },

    async abrirModal(action, chamado){

      this.action = action;

      if(action==1){
        this.chamado = "";
        this.description = "",
        this.area = null;
        this.status = this.optionsStatus[0];
        this.nivel = null;
        this.dataObjeto = new Date();
        this.dataHoje = this.dataObjeto.getDate() + '/' + this.dataObjeto.getMonth() + '/' + this.dataObjeto.getFullYear();

        const userId = this.getCookie('user');
        let loggedUser = await axios.get("http://127.0.0.1:3000/usuario/loggedUser", {params:{id:userId}});
        this.usuario = loggedUser.data.name;
      }else if(action == 0){
        let chamadoObj = JSON.parse(JSON.stringify(chamado));

        this.chamado = chamadoObj.chamado;
        this.description = chamadoObj.descricao,
        this.area = this.optionsArea[chamadoObj.area];
        this.nivel = this.optionsNivel[chamadoObj.nivel];
        this.status = this.optionsStatus[chamadoObj.status];
        this.oldStatus = JSON.parse(JSON.stringify(this.status));
        this.dataHoje = chamadoObj.data;
        this.usuario = chamadoObj.User.user;
        this.id = chamadoObj.codigo;
      }
    },

    open(evt, row){
      if (row!=null){
        this.abrirModal(0, row);
      }else{
        this.abrirModal(1, null);
      }

      this.addModal = true;
    }
  }
})
</script>

<style lang="scss" scoped>
@media screen and (min-width: 920px) {
  body{
    margin-top: 48px;
    min-width: 920px;
    height: calc((100vh - 48px) - 50px) !important;
  }
  #body{
    width: 100%;
    background: linear-gradient(45deg, #03045E, #00B4D8, #90E0EF, #CAF0F8);
    background-size: 200% 200%;
    animation: colors 15s both infinite;
  }
  .head{
    display: flex;
    width: 100%;
    height: 60px;
    padding: 2px 10px;
    align-items: center;
    p{
        font-size: 16px;
    }
    button{
        height: 36px;
    }
  }
  .other-user{
    width: 100%;
    display: flex;
    justify-content: flex-end;
  }
  .panel-actions{
      background: var(--q-primary);
      height: calc(100% - 120px);
      width: 95%;
      padding: 20px;
      margin: 0 auto;
      border-radius: 20px;
      box-shadow: rgba(0, 0, 0, 0.16) 0px 3px 6px, rgba(0, 0, 0, 0.23) 0px 3px 6px;
  }
  .chamados{
      height: 100%;
  }
  .q-table__container{
    background: none;
    box-shadow: none;
    height: 76.34%;
  }
  .btn-actions{
      width: 100%;
      height: calc(100% - 405px);
      display: flex;
      align-items: center;
      justify-content: center;
      button{
          height: 36px;
          margin: 20px;
      }

  }
  .modal-title{
      display: flex;
      width: 100%;
      justify-content: center;
      align-items: center;
  }
  .header-content{
    display: flex;
    justify-content: center;
      p{
          margin: 0px 20px;
          font-size: 16px;
      }
      label{
          width: 200px;
      }
  }
  .header-content{
    .chamados, .datas, .users{
        padding: 10px 1.1rem;;
    }
  }
  .body-content{
    display: flex;
    width: 100%;
    justify-content: center;
    p{
        margin: 0px 20px;
        font-size: 16px;
    }
    label{
        width: 200px;
      }
    .area, .status, .nivel{
        padding: 10px 1.1rem;;
    }
  }
  .modal-content{
    max-width: 60% !important;
    max-height: 100% !important;
  }
  .descript{
    margin: 0 auto;
    width: 90%;
    p{
        margin: 5px 0;
    }
  }
  .uploadDoc{
    margin: 0 auto;
    width: 90%;
    p{
        margin: 15px 0px 5px 0;
    }
  }
  .actions{
    margin: 0 auto;
    width: 90%;
    p{
        margin: 15px 0px 5px 0;
    }
  }
  .q-card__section--vert{
      padding: 8px !important;
  }
}


// mobiles
@media screen and (max-width: 920px) {

}


// animation
@keyframes colors {
  0%{
    background-position: 0% 50%;
  }

  50%{
    background-position: 100% 50%;
  }

  100%{
    background-position: 0% 50%;
  }
}
</style>
