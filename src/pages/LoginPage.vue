<template>
<Header>
    <body>
        <div id="login">

        </div>
    </body>
</Header>
<Footer>

</Footer>
</template>

<script>
import { defineComponent, ref } from 'vue';
import Header from '../layouts/Header.vue';
import Footer from '../layouts/Footer.vue';

export default defineComponent({
  name: 'LoginPage',
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
body{
    min-width: 920px;
    min-height: calc((100vh - 48px) - 50px) !important;
    display: flex;
    margin-top: 48px;
}
</style>