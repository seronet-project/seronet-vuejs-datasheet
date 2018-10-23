<template>
  <v-list-tile-content>
    <v-list-tile-sub-title class="grey--text text--darken-4">
      <a :href="field.value">{{ field.name }} to {{linkSuffix}}</a>
    </v-list-tile-sub-title>
  </v-list-tile-content>
</template>
<script>
import {match, nth, compose, toUpper} from 'ramda'
export default {
  props:['field'],
  computed: {
    linkSuffix() {
      return compose(
        toUpper,
        nth(1),
        match(/\.([a-zA-Z0-9]+)$/)
      )(this.field.value)
    }
  }
}
</script>
