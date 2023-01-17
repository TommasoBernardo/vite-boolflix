<script>
import { store } from './store.js'
import ComponentsHeader from './components/ComponentsHeader.vue'
import ComponentsMain from './components/ComponentsMain.vue'



export default{
  name: 'App.vue',
  components : {
    ComponentsHeader,
    ComponentsMain,
  },
  data(){
    return{
      store,
    }
  }
}
</script>

<template>
<ComponentsHeader />
    <link rel="stylesheet" 
        href="https://use.fontawesome.com/releases/v5.2.0/css/all.css" 
        integrity="sha384-hWVjflwFxL6sNzntih27bfxkr27PmbbK/iSvJ+a4+0owXq79v+lsFkW54bOGbiDQ" 
        crossorigin="anonymous">
<ComponentsMain />

</template>

<style lang="scss">
@use './styles/general.scss' as *; 
@use './styles/partials/variables' as *; 
</style>
