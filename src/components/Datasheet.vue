<template>
<v-layout>
  <v-flex xs12 sm6 offset-sm3>
    <v-card>
      <v-toolbar color="pink" dark>
        <v-toolbar-side-icon></v-toolbar-side-icon>
        <v-toolbar-title>Component Datasheet ({{componentId}})</v-toolbar-title>
        <v-spacer></v-spacer>
        <v-btn icon>
          <v-icon>search</v-icon>
        </v-btn>
        <v-btn icon>
          <v-icon>check_circle</v-icon>
        </v-btn>
      </v-toolbar>
      <div v-for="(section, index) in sections" :key="index">
        <ds-section v-bind="section"/>
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
  props: ['componentId', 'sections']
}
</script>
