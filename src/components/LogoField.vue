<template>
  <v-list-tile-content>
    <v-list-tile-sub-title class="grey--text text--darken-4">
      <img :src="field.value.url" :title="field.value.title"/>
    </v-list-tile-sub-title>
  </v-list-tile-content>
</template>
<script>
export default {
  props:['field']
}
</script>
