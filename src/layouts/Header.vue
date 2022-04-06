<template>
  <q-layout view="hHh lpR fFf" style="min-height: calc(100vh - 48px - 50px) !important;">
    <q-header reveal elevated class="text-white bgcolor-primary" >
      <q-toolbar>
        <q-toolbar-title>
          <p>BeDesk</p>
        </q-toolbar-title>
      </q-toolbar>
    </q-header>
    <slot></slot>
  </q-layout>
</template>
<script>
import { defineComponent, ref } from 'vue'

export default defineComponent({
  name: 'Header',


  setup () {
    const DrawerOpen = ref(false)

    return {
      DrawerOpen,
      toggleDrawer () {
        DrawerOpen.value = !DrawerOpen.value
      }
    }
  }
})
</script>
<style lang="scss" scoped>

p{
  font-size: 2rem;
  margin: auto !important;
}
.q-toolbar__title{
  display: flex;
  align-items: center;
  place-content: center;
  font-family: "Lobster";
  font-size: 36px;
  text-shadow: 0px 4px 3px rgba(0,0,0,0.4),
             0px 8px 13px rgba(0,0,0,0.1),
             0px 18px 23px rgba(0,0,0,0.1);
}
</style>
