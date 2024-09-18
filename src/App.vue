<script>

  import AppHeader from './components/AppHeader.vue';
  import AppMain from './components/AppMain.vue';
  import AppFooter from './components/AppFooter.vue';

  export default {
      data() {
        return { 
          message: 'hello'
        }
      },
      methods: {

      },
      components:{
        AppHeader,
        AppMain,
        AppFooter,
      }
  }
</script>

<template>

  <div>
    <AppHeader/>
  </div>
  <div>
    <AppMain/>
  </div>
  <div>
    <AppFooter/>
  </div>

</template>

<style lang="scss">

@use 'assets/scss/main' as *;

// Import all of Bootstrap's CSS
@import "bootstrap/scss/bootstrap";

</style>
