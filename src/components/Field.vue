<template>
<v-list-tile avatar ripple>
  <v-list-tile-content>
    <v-list-tile-title>{{ name }}</v-list-tile-title>
    <v-list-tile-sub-title class="grey--text text--darken-4">
      <a v-if="type == 'URL'" :href="value">{{ name }} to {{linkSuffix}}</a>
      <div v-else-if="type == 'QUANTITY'"> {{value.quantity}}&nbsp;{{value.unit}} </div>
      <img v-else-if="type == 'IMAGE'" :src="value.url" :title="value.title" /> <!-- Logo/Image -->
      <div v-else>{{value}}</div>
    </v-list-tile-sub-title>
  </v-list-tile-content>
  <v-list-tile-action>
    <v-list-tile-action-text>{{type}}</v-list-tile-action-text>
  </v-list-tile-action>
</v-list-tile>
</template>
<script>
export default {
  components: {},
  props: ['name', 'type', 'value']
}
</script>
