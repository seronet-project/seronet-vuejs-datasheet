<template>
<div>
  <v-toolbar color="blue" dark>
    <v-icon>{{mdicon}}</v-icon>
    <v-spacer></v-spacer>
    <v-toolbar-title>
      {{name}}
    </v-toolbar-title>
    <v-spacer></v-spacer>
  </v-toolbar>
  <v-list two-line>
    <ds-field></ds-field>
    <div v-for="(field, index) in fields" :key="index">
      <ds-field v-bind="field" />
      <v-divider />
    </div>
  </v-list>
</div>
</template>
<script>
import DsField from "./Field"

export default {
  components: {
    DsField
  },
  props: ['mdicon', 'name', 'fields']
}
</script>
