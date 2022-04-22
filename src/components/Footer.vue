<template>
  <q-layout style="min-height: auto;">

    <q-page-container>
      <router-view />
    </q-page-container>

    <q-footer elevated class="bg-primary">
      <q-toolbar>
        <slot></slot>
      </q-toolbar>
    </q-footer>

  </q-layout>
</template>

<script>
import { defineComponent } from 'vue'

export default defineComponent({
  name: 'Footer',


  setup () {

  }
})
</script>
<style lang="scss" scoped>
text{
  font-family: 'Rubik', sans-serif;
}
.q-page-container{
  padding-bottom: 0px !important;
}
.absolute-bottom{
  bottom: auto !important;
}
</style>
