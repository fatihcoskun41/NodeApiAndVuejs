<template>
<Form></Form>
<List></List>
</template>

<script>
  import Form from './components/Form.vue'
  import List from './components/List.vue'

export default {

  name: 'App',
  components: {
    Form,
    List

  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin:0 auto;
 width:500px
}
</style>
