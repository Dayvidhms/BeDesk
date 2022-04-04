<template>
  <header>
    <div class="header">
      <h1>BeDesk</h1>
      <h3>Seu novo serviço de Help Desk!</h3>
        <br>
        <q-btn color="primary" label="Cadastrar" />
        <q-btn color="primary" label="Acessar" />
      </div>
  </header>

  <body>
    <div class="body-content">
      <div class="about-program">
        <img class="img-analysis" src="../assets/analysis-img.svg" alt="Pessoa com um mapa em sua frente e alguns pontos marcados para analise">
          <div class="text-about">
            <p>Não sofra, encontre sua solução com BeDesk</p>
          </div>
            <img class="img-search" src="../assets/search-img.svg" alt="Pessoa com um mapa em sua frente e alguns pontos marcados para analise">
      </div>
    </div>
  </body>

  <footer>
    <div class="footer">
    </div>
  </footer>

</template>

<script>
import { defineComponent } from 'vue'

export default defineComponent({
  name: 'IndexPage'
})
</script>

<style lang="scss" scoped>
*{padding: 0; margin: 0; box-sizing: border-box;}
body{
  padding-top: 2rem;
}
.body-content{
  max-width: 100%;
}
.about-program{
  font-family: 'DM Serif Display', serif;
  display: flex;
  font-size: 20px;
  width: 100%;
  height: 250px;
  margin-top: 2rem;
  text-align: center;
  justify-content: center;
  align-items: flex-start;
}

.text-about{
  font-size: 24px;
  p{
    font-family: 'Cabin', sans-serif;
  }
  
}

.img-analysis{
  width: 35%;
  height: 370px;
  position: relative;
  top: -100px;
}

.img-search{
  width: 35%;
  height: 370px;
  position: relative;
  top: -100px;
}

img{
  max-width: 100%;
}

header {
	background: #57BEE6;
	text-align: center;
	width: 100%;
	height: auto;
	background-size: cover;
	background-attachment: fixed;
	position: relative;
	overflow: hidden;
	border-radius: 0 0 85% 85% / 30%;
}
header .header{
	width: 100%;
	height: 100%;
	padding: 10px 50px 50px 50px;
	color: #FFF;
	text-shadow: 1px 1px 1px #333;
}

h1 {
  font-family: 'Lobster', cursive;
	font-size: 80px;
	margin-bottom: 30px;
}

h3, p{
  font-family: 'Kalam', cursive;
}

button {
  width: 150px;
  margin: 5px;
	padding: 10px 20px;
	border-radius: 50px;
	box-shadow: 0 3px 20px 0 #0000003b;
}
button:hover{
	cursor: pointer;
}


footer {
	background: #57BEE6;
	text-align: center;
	width: 100%;
	height: auto;
	background-size: cover;
	background-attachment: fixed;
	position: relative;
	overflow: hidden;
	border-radius: 85% 85% 0 0 / 100%;
  bottom: -96px;
}
footer .footer{
	width: 100%;
	padding: 50px;
	color: #FFF;
	text-shadow: 1px 1px 1px #333;
}
</style>
