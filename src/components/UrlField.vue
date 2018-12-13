<template>
  <v-list-tile-content>
    <v-list-tile-sub-title class="grey--text text--darken-4">
      <a :href="field.value">{{ field.name }} to {{linkSuffix}}</a>
    </v-list-tile-sub-title>
  </v-list-tile-content>
</template>
<script>
import {match, compose} from 'ramda'
export default {
  props:['field'],
  computed: {
    linkSuffix() {
      return compose(
        x => match(/\.([a-zA-Z0-9]+)$/)(x)[1] || x
      )(this.field.value)
    }
  }
}
</script>
