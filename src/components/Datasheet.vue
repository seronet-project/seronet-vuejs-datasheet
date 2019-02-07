<template>
<v-layout>
  <v-flex xs12 sm6 offset-sm3>
    <v-card>
      <v-toolbar :color="this.color" dark>
        <v-toolbar-title>Component Datasheet ({{componentId}})</v-toolbar-title>
        <v-spacer></v-spacer>
      </v-toolbar>
      <div v-for="(section, index) in sections" :key="index">
        <ds-section
          color="blue"
          v-bind="section"
        ></ds-section>
      </div>
    </v-card>
  </v-flex>
</v-layout>
</template>

<script>
import DsSection from './Section'

export default {
  components: {
    DsSection
  },
  props: {
    color: String,
    componentId: String,
    sections: null
  }
}
</script>
