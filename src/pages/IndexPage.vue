<template>
  <Header> 
      <body class="gradient">
        <div id="index">
          <div class="body-content">
            <div class="about-program">
              <img class="img-analysis" src="../assets/analysis-img.svg" alt="Pessoa com um mapa em sua frente e alguns pontos marcados para analise">
                  <div class="group-text-btn">
                    <div class="text-about">
                        <p>Não sofra, encontre sua solução com BeDesk</p>
                    </div>
                    <div class="btn-group-index">
                        <q-btn text-color="primary" color="white" label="Cadastrar" />
                        <q-btn color="primary" label="Acessar" />
                    </div>
                  </div>
                <img class="img-search" src="../assets/search-img.svg" alt="Pessoa com um mapa em sua frente e alguns pontos marcados para analise">
            </div>
          </div>
        </div>
      </body>
  </Header>
  <Footer>
    <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24"><path d="M12 0c-6.626 0-12 5.373-12 12 0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23.957-.266 1.983-.399 3.003-.404 1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576 4.765-1.589 8.199-6.086 8.199-11.386 0-6.627-5.373-12-12-12z"/></svg> 
    
  </Footer>
</template>

<script>
import { defineComponent, ref } from 'vue';
import Header from '../layouts/Header.vue';
import Footer from '../layouts/Footer.vue';

export default defineComponent({
  name: 'IndexPage',
  components: {
    Header,
    Footer
  },
  setup () {

    return {

    }
  }
})
</script>

<style lang="scss" scoped>

*{padding: 0; margin: 0; box-sizing: border-box;}

// Desktops
@media screen and (min-width: 920px) {
  #index{
  min-width: 920px;
  min-height: calc((100vh - 48px) - 50px) !important;
  display: flex;
  }
  .gradient{
    margin-top: 48px;
    background: linear-gradient(45deg, #03045E, #00B4D8, #90E0EF, #CAF0F8);
    background-size: 500% 500%;
    animation: colors 15s both infinite;
    height: 100%;
    width: 100%;
  }

  .body-content{
    display: flex;
    align-items: center;
    justify-content: center;
    height: 100%;
    width: 100%;
    padding: 2rem;
    margin: auto;
  }

  .about-program{
    display: flex;
    height: 100%;
    width: 100%;
  }

  .group-text-btn{
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    padding: 1rem;
      p{
        font-family: 'DM Serif Display';
        font-size: 24px;
        padding: .4rem;
        color: white !important;
        -webkit-background-clip: text;
        -moz-background-clip: text;
        background-clip: text;
        text-align: center;
        text-shadow: 2px 4px 3px rgba(0,0,0,0.3);
      }
      button {
        width: 100%;
        margin: 5px;
        padding: 10px 20px;
        border-radius: 50px;
        box-shadow: 0 3px 20px 0 #0000003b;
      }
      }

      .menu-btn{
        padding: 20px;
      }

      img{
        max-height: 100%;
        display: flex;
        max-width: 100%;
        min-width: 150px;
        margin: auto;
      }
    .btn-group-index{
      width: 100%;
      display: flex;
      justify-content: center;
      align-items: center;
    }
  } 

 // Mobiles
@media screen and (max-width: 920px) {
  #index{
  max-height: 100%;
  max-width: 920px;
  padding: 0.5em;
  width: 100%;
  height: 100%;
  }
  .gradient{
    display: flex;
    align-items: center;
    justify-content: center;
    margin-top: 48px;
    background: linear-gradient(45deg, #03045E, #00B4D8, #90E0EF, #CAF0F8);
    background-size: 500% 500%;
    animation: colors 15s both infinite;
    height: 100%;
    width: 100%;
  }

  .body-content{
    margin: auto;
  }
  .group-text-btn{
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
      p{
        font-family: 'DM Serif Display';
        font-size: 24px;
        padding: .4rem;
        color: white !important;
        -webkit-background-clip: text;
        -moz-background-clip: text;
        background-clip: text;
        text-align: center;
        text-shadow: 2px 4px 3px rgba(0,0,0,0.3);
      }
      button {
        margin: 5px;
        padding: 10px 20px;
        border-radius: 50px;
        box-shadow: 0 3px 20px 0 #0000003b;
        width: 100%;
      }
    }

      .menu-btn{
        padding: 20px;
        height: 100%;
        width: 100%;
      }

      img{
        max-width: 920px;
        max-height: 100%;
        width: 100%;
        display: flex;
        margin: auto;
      }
  .group-text-btn{
    padding: 2rem;
    height: 100%;
    width: 100%;
  }
  .btn-group-index{
    display: flex;
    flex-direction: column;
    height: 100%;
    width: 100%;
    align-items: center;
    justify-content: center;
  }
}

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
