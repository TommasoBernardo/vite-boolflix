<script>
import ComponentsHeader from './components/ComponentsHeader.vue'
import ComponentsMain from './components/ComponentsMain.vue'

export default{
  name: 'App.vue',
  components : {
    ComponentsHeader,
    ComponentsMain
  }
}
</script>

<template>
<ComponentsHeader />

<ComponentsMain />

</template>

<style lang="scss" scoped>
@use './styles/general.scss' as *; 
</style>
