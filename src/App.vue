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

<ComponentsMain />

</template>

<style lang="scss">
@use './styles/general.scss' as *; 
@use './styles/partials/variables' as *; 
</style>
