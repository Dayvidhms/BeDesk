<template>
<Header>
    <body id="body">
      <div class="img-login">
        <div id="login">
          <q-card class="my-card bg-primary  login-card">
            <q-card-section>
              <div class="text-h6 header-login"> Login </div>
            </q-card-section>

          <div >
            <q-card-actions>
              <div class="q-pa-md dados-login" style="max-width: 400px">
                <q-form
                  @submit="onSubmit"
                  class="q-gutter-md form-login"
                >
                  <q-input
                    dark
                    label-color="white"
                    color="white"
                    filled
                    v-model="user"
                    label="Usuário *"
                    lazy-rules
                    :rules="[ val => val && val.length !== '' || 'Por favor informe seu usuário',
                    ]"
                  />

                  <q-input
                    dark
                    label-color="white"
                    color="white"
                    filled
                    type="password"
                    v-model="password"
                    label="Senha *"
                    lazy-rules
                    :rules="[
                      val => val !== null && val !== '' || 'Por favor insira sua senha',
                    ]"
                  />

                  <div class="login-settings">
                    <a>Esqueceu sua senha?</a>
                    <a @click="redirectTo('/cadastro')">Ainda não tem cadastro? Increva-se agora!</a>
                  </div>

                  <div>
                    <q-btn label="Entrar" type="submit" color="primary" @click.prevent="userLogin()"/>
                  </div>
                </q-form>
              </div>
            </q-card-actions>
          </div>
          </q-card>
        </div>
      </div>
    </body>
</Header>
<Footer>

</Footer>
</template>

<script>
import { useQuasar} from 'quasar';
import { defineComponent, ref } from 'vue';
import { useRouter } from 'vue-router';
import Header from '../components/Header.vue';
import Footer from '../components/Footer.vue';

import axios from 'axios';
import swal from 'sweetalert';

export default defineComponent({
  name: 'LoginPage',
  components: {
    Header,
    Footer
  },
  setup () {
    const $q = useQuasar()

    const user = ref(null)
    const password = ref(null)

    const router = useRouter();

    const redirectTo = (view) => {
      router.push({ path : view});
    }

    return {
      user,
      password,
      redirectTo,

      onSubmit () {

      }

    }
  },

    methods:{
      userLogin(){
        const postData = {user: this.user, password: this.password};

          axios.post("http://127.0.0.1:3000/usuario/login", postData)
          .then(res=>{

            if(res.data.value != 0){
                swal({
              title: "Logado com sucesso.",
              text: "Você será redirecionado para a tela de gestão de chamados.",
              icon: "success",
              button: "Ok",
            }).then(()=>{
              document.cookie='user=' + res.data.userId;
              document.cookie='tipo=' + res.data.tipo;
            })
            .then(()=>this.redirectTo('/gestao'));

            }else{
            swal({
              title: "Credenciais incorretas.",
              text: "Senha ou usuário incorretos.",
              icon: "error",
              button: "Ok",
          });
            }
          })
          .catch(error=>console.log(error));
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
    display: flex;
    width: 100%;
    background: linear-gradient(45deg, #03045E, #00B4D8, #90E0EF, #CAF0F8);
    background-size: 200% 200%;
    animation: colors 15s both infinite;
  }

  .img-login{
    width: 100%;
    background-image: url("../assets/login-img.svg");
    background-repeat: no-repeat;
    background-size: 60%;
    background-position: center;
  }

  #login{
    justify-content: center;
    align-items: center;
    display: flex;
    margin: auto;
    width: 90%;
    height: 100%;
    z-index: 2000;
  }
  .login-card{
    display: flex;
    text-align: center;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    height: 70%;
    width: 30%;
    color: white;
  }
  .header-login{
    display: flex;
    justify-content: center;
    align-items: center;
    font-family: 'Fredoka One', cursive;
    font-size: 36px;
    text-shadow: 2px 4px 3px rgba(0,0,0,0.3);
  }
  .form-login{
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;

    .q-field{
      padding: 0.1rem ;
    }

    a{
      margin-bottom: 5px;
      cursor: pointer;
    }
  }
  .login-settings{
    margin: 0.5rem;
    display: grid;
  }


}


// mobiles
@media screen and (max-width: 920px) {
  body{
    margin-top: 48px;
    max-width: 920px;
    height: calc((100vh - 48px) - 50px) !important;
  }
  #body{
    display: flex;
    width: 100%;
    background: linear-gradient(45deg, #03045E, #00B4D8, #90E0EF, #CAF0F8);
    background-size: 200% 200%;
    animation: colors 15s both infinite;
  }

  .img-login{
    width: 100%;
    background-image: url("../assets/login-img.svg");
    background-repeat: no-repeat;
    background-size: 95%;
    background-position: center;
  }

  #login{
    justify-content: center;
    align-items: center;
    display: flex;
    margin: auto;
    width: 100%;
    height: 100%;
    z-index: 2000;
  }
  .login-card{
    display: flex;
    text-align: center;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    height: auto;
    max-width: 95%;
    width: auto;
    color: white;
  }
  .header-login{
    display: flex;
    justify-content: center;
    align-items: center;
    font-family: 'Fredoka One', cursive;
    font-size: 36px;
    text-shadow: 2px 4px 3px rgba(0,0,0,0.3);
  }
  .form-login{
    display: flex;
    align-items: center;
    justify-content: center;
    flex-direction: column;

    .q-field{
    }

    a{
      margin-bottom: 5px;
      cursor: pointer;
    }
  }
  .login-settings{
    margin: 0.5rem;
    display: grid;
  }



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
