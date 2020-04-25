<template>
<div>
<Navbar/>
<div class="container">
  <router-view/>
</div>
<Footer/>
</div>
</template>
<script>
import Navbar from './components/Navbar';
import Footer from './components/Footer'
export default {
  components: {
    Navbar,
    Footer,
  }
}
</script>
<style>
body{
  font-family: Arial, Helvetica, sans-serif;
}
.mg-top {
  margin-top: 32px;
}
</style>
