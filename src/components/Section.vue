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
    <div v-for="field in (showLess ? fields.slice(0, 5) : fields)" :key="field.name + Math.random()">
        <ds-field v-bind="field" />
        <v-divider />
    </div>
    <v-btn block color="secondary" dark @click="showLess = !showLess" v-if="fields.length > 5">
      <v-icon v-if="showLess">expand_more</v-icon>
      <v-icon v-else>expand_less</v-icon>
    </v-btn>
  </v-list>
</div>
</template>
<script>
import DsField from "./Field.vue"

export default {
  components: {
    DsField
  },
  data() {
    return {
      showLess: true
    }
  },
  props: {
    color: String,
    mdicon: String,
    name: String,
    fields: null
  }
}
</script>
