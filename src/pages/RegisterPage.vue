<template>
<Header>
    <body id="body">
      <div class="img-register">
        <div id="register">
          <q-card class="my-card bg-primary  register-card">
            <q-card-section>
              <div class="text-h6 header-register"> Registrar </div>
            </q-card-section>

          <div >
            <q-card-actions>
              <div class="q-pa-md dados-register" style="max-width: 400px">
                <q-form
                  @submit="onSubmit"
                  class="q-gutter-md form-register"
                > 
                  <div class="names form-register">
                    <q-input
                      dark
                      label-color="white"
                      color="white"
                      filled
                      v-model="name"
                      label="Nome"
                      lazy-rules
                      :rules="[ val => val && val.length !== '' || 'Por favor informe seu usuário',
                      ]"
                    />
                    <q-input
                      dark
                      label-color="white"
                      color="white"
                      filled
                      v-model="underName"
                      label="Sobrenome"
                      lazy-rules
                      :rules="[ val => val && val.length !== '' || 'Por favor informe seu usuário',
                      ]"
                    />
                  </div>
                  <div class="form-register">
                    <q-input
                      dark
                      label-color="white"
                      color="white"
                      filled
                      v-model="user"
                      label="Usuário"
                      lazy-rules
                      :rules="[ val => val && val.length !== '' || 'Por favor informe seu usuário',
                      ]"
                    />
                    <q-input
                      dark
                      label-color="white"
                      color="white"
                      filled
                      v-model="mail"
                      label="Email"
                      lazy-rules
                      :rules="[ val => val && val.length !== '' || 'Por favor informe seu usuário',
                      ]"
                    />
                  </div>
                  <div class="form-register form-password">
                    <q-input
                      dark
                      label-color="white"
                      color="white"
                      filled
                      v-model="password"
                      label="Senha"
                      lazy-rules
                      :rules="[ val => val && val.length !== '' || 'Por favor informe seu usuário',
                      ]"
                    />
                    <q-input
                      dark
                      label-color="white"
                      color="white"
                      filled
                      v-model="password2"
                      label="Repita a senha"
                      lazy-rules
                      :rules="[ val => val && val.length !== '' || 'Por favor informe seu usuário',
                      ]"
                    />
                  </div>
                  <div class="option-form">
                    <q-select class="select-form" dark filled v-model="model" :options="options" label="Tipo de usuário" />
                  </div>
                  <div class="button-form">
                    <q-btn text-color="primary" color="white" label="Limpar" @click="redirectTo('/cadastro')"/>
                    <q-btn color="primary" label="Confirmar" @click="redirectTo('/login')" />
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
import { useRouter } from 'vue-router';
import { defineComponent, ref } from 'vue';
import Header from '../layouts/Header.vue';
import Footer from '../layouts/Footer.vue';

export default defineComponent({
  name: 'RegisterPage',
  components: {
    Header,
    Footer
  },
  setup () {

    const name = ref(null)
    const underName = ref(null)
    const mail = ref(null)
    const user = ref(null)
    const password2 = ref(null)
    const password = ref(null)

    const router = useRouter();

    const redirectTo = (view) => {
      router.push({ path : view});
    }

    return {
      name,
      underName,
      user,
      mail,
      password,
      password2,
      model: ref(),
      options: [
        'Atendente', 'Usuário'
      ],

      onSubmit () {

      },
      redirectTo
    
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

  .img-register{
    width: 100%;
    background-image: url("../assets/register.svg");
    background-repeat: no-repeat;
    background-size: 50%;
    background-position: bottom right;
  }
  
  #register{
    justify-content: center;
    align-items: center;
    display: flex;
    margin: auto;
    width: 90%;
    height: 100%;
    z-index: 2000;
  }
  .register-card{
    display: flex;
    text-align: center;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    height: auto;
    width: auto;
    color: white;
  }
  .header-register{
    display: flex;
    justify-content: center;
    align-items: center;
    font-family: 'Fredoka One', cursive;
    font-size: 36px;
    text-shadow: 2px 4px 3px rgba(0,0,0,0.3);
  }
  .form-register{
    display: flex;
    align-items: center;
    justify-content: center;
    margin-bottom: 5px;
    .q-field{
      padding: 0.1rem ;
    }

    a{
      margin-bottom: 5px;
      cursor: pointer;
    }
  }
  .register-settings{
    margin: 0.5rem;
    display: grid;
  }
  .q-form{
    flex-direction: column;
  }
  .option-form{
    width: 100%;
    display: block;
    margin: 0px auto;
    padding-left: 15px;
  }
  .select-form{
    min-width: 100%;
  }
  .form-password{
    padding-bottom: 16px;
  }
  .button-form{
    width: 100%;
    display: flex;
    justify-content: center;
    button{
      margin-left: 20px;
      width: 100px;
    }
  }
}


// mobiles 
@media screen and (max-width: 920px) {
  body{
    margin-top: 48px;
    max-width: 920px;
    height: 100%;
    height: calc((100vh - 48px) - 50px) !important;
  }
  #body{
    display: flex;
    width: 100%;
    background: linear-gradient(45deg, #03045E, #00B4D8, #90E0EF, #CAF0F8);
    background-size: 200% 200%;
    animation: colors 15s both infinite;
  }

  .img-register{
    width: 100%;
    background-repeat: no-repeat;
    background-size: 95%;
    background-position: center;
  }
  
  #register{
    justify-content: center;
    align-items: center;
    display: flex;
    margin: auto;
    width: 100%;
    height: 100%;
    z-index: 2000;
    padding: 15px;
  }
  .register-card{
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
  .header-register{
    display: flex;
    justify-content: center;
    align-items: center;
    font-family: 'Fredoka One', cursive;
    font-size: 36px;
    text-shadow: 2px 4px 3px rgba(0,0,0,0.3);
  }
.form-register{
    display: flex;
    align-items: center;
    justify-content: center;
    margin-bottom: 5px;
    .q-field{
      padding: 0.1rem ;
    }

    a{
      margin-bottom: 5px;
      cursor: pointer;
    }
  }
  .register-settings{
    margin: 0.5rem;
    display: grid;
  }
  .q-form{
    flex-direction: column;
  }
  .option-form{
    width: 100%;
    display: block;
    margin: 0px auto;
    padding-left: 15px;
  }
  .select-form{
    min-width: 100%;
  }
  .form-password{
    padding-bottom: 16px;
  }
  .button-form{
    width: 100%;
    display: flex;
    justify-content: center;
    button{
      margin: 0 auto;
      width: 100px;
    }
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