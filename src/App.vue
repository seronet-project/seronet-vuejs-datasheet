<template>
  <v-app>
    <v-text-field solo autofocus full-width v-model="componentId"/>

    <!--Language Buttons  -->
    <Actionbar :componentId="componentId" @update="handleClickInParent"/>

    <Datasheet :componentId="componentId" :sections="sections"/>


  </v-app>
</template>

<script>
import Datasheet from './components/Datasheet'
import Actionbar from './components/Actionbar'

export default {
  components: {
    Datasheet, Actionbar
  },
  data() {
    return {
      componentId: "http://servicerobotik-ulm.de/ComponentsAndSystems#SmartCdlServer",
      sections: []
    }
  },
  methods: {
    handleClickInParent(sections) {
      this.sections = sections
  }
  //...
}
}
</script>
