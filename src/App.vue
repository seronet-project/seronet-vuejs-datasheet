<template>
  <v-app>
    <v-text-field solo autofocus full-width v-model="componentId"/>
    <Datasheet :componentId="componentId"/>
  </v-app>
</template>

<script>
import Datasheet from './components/Datasheet'
export default {
  components: {
    Datasheet
  },
  data() {
    return {
      componentId: "http://seronet/example/rb1"
    }
  }
}
</script>
