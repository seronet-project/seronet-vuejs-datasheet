<template>
<div>
  <v-toolbar :color="this.color" dark>
    <v-icon>{{mdicon}}</v-icon>
    <v-spacer></v-spacer>
    <v-toolbar-title>
      {{name}}
    </v-toolbar-title>
    <v-spacer></v-spacer>
  </v-toolbar>
  <v-list two-line>
    <div v-for="(field, index) in fields" :key="index">
      <ds-field v-bind="field" />
      <v-divider />
    </div>
  </v-list>
</div>
</template>
<script>
import DsField from "./Field.vue"

export default {
  components: {
    DsField
  },
  props: {
    color: String,
    mdicon: String,
    name: String,
    fields: null
  }
}
</script>
