<template>
  <Header/>
  <div class="container">
    <router-view/>
  </div>
</template>

<script>
// @ is an alias to /src
import Header from './components/Header'

export default {
  name: 'App',
  components: {
    Header,
  }
}
</script>
