<template>
  <v-app dark>
    <v-toolbar app color="primary">
      <v-toolbar-title v-text="title"></v-toolbar-title>
    </v-toolbar>
    <v-content>
      <HelloWorld />
    </v-content>
    <v-footer app>
      <span>&copy; Jake made dis</span>
    </v-footer>
  </v-app>
</template>

<script>
import HelloWorld from './components/HelloWorld'

export default {
  name: 'App',
  components: {
    HelloWorld
  },
  data () {
    return {
      title: 'Who Gets the Phone ?'
    }
  }
}
</script>
