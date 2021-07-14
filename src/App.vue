<template>
  <div id="nav">
    <Navbar />
    <router-view />
  </div>
</template>

<style>

</style>


<script>

  import Navbar from '@/components/Navbar';

  export default{
    components:{
      Navbar,
    }
  }

</script>

