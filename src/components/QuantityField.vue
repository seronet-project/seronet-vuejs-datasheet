<template>
  <v-list-tile-content>
    <v-list-tile-title>{{ field.name }}</v-list-tile-title>
    <v-list-tile-sub-title class="grey--text text--darken-4">
      {{field.value.quantity}}&nbsp;{{field.value.unit}}
    </v-list-tile-sub-title>
  </v-list-tile-content>
</template>
<script>
export default {
  props:['field']
}
</script>
